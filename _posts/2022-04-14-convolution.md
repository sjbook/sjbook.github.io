---
layout: single
title : "5.Convolution"
author_profile: true
categories: DL
tag: [python, pytorch, deeplearning]
toc: true
use_math: true
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }
    
    table.dataframe td {
      text-align: center;
      padding: 8px;
    }
    
    table.dataframe tr:hover {
      background: #b8d1f3; 
    }
    
    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>


# Convolution Layer


## Convolution


### 1개 채널

![convolution_calc](../../images/2022-04-14-convolution/convolution_calc.jpg)

### 여러개 채널

![multi_channel_conv](../../images/2022-04-14-convolution/multi_channel_conv.jpg)

## 패딩

![padding](../../images/2022-04-14-convolution/padding-16499201678874.jpg)

## 특성

![conv2](../../images/2022-04-14-convolution/conv2.jpg)

## Shape


\\(O_{h} = floor({I_{h} - K_{h} + 2P \over S} + 1)\\)



\\(O_{w} = floor({I_{w} - K_{w} + 2P \over S} + 1)\\)



\\(O_{h}, O_{w} = \\)피처맵의 높이, 너비



\\(I_{h}, I_{w} = \\) 인풋의 높이, 너비



\\(K_{h}, K_{w} = \\)커널의 높이, 너비



\\(P = \\)패딩 사이즈



\\(S = \\)스트라이드(보폭)



floor => 소수점 이하 버림



![conv_shape](../../images/2022-04-14-convolution/conv_shape.jpg)

pytorch에서 conv layer를 사용하기 위해서는



(배치사이즈, 채널수, 높이, 너비)의 차원으로 인풋 이미지를 준비해야 한다.



[Conv Layer](https://pytorch.org/docs/stable/generated/torch.nn.Conv2d.html)의 argument로는 (in_channels, out_channels, kernel_size)를 넘겨준다.


## 실습


### Shape of Conv Layers



```python
import torch

N, I_h, I_w, C_i = 1, 28, 28, 5
n_filter = 1
k_size = 3

images = torch.rand(N, C_i, I_h, I_w)
conv = torch.nn.Conv2d(C_i, n_filter, kernel_size = k_size)

y = conv(images)

W = conv.weight
B = conv.bias

print(images.shape)
print(W.shape)
print(B.shape)
print(y.shape)
```

<pre>
torch.Size([1, 5, 28, 28])
torch.Size([1, 5, 3, 3])
torch.Size([1])
torch.Size([1, 1, 26, 26])
</pre>
### Convolution Calculatation



```python
import numpy as np
import torch

N, I_h, I_w, C_i = 1, 5, 5, 1
n_filter = 1
k_size = 3

images = torch.rand(N, C_i, I_h, I_w)
conv = torch.nn.Conv2d(C_i, n_filter, kernel_size = k_size)

y = conv(images)
print("Y(Pytorch) : \n", y.detach().numpy().squeeze())
W = conv.weight
B = conv.bias

images = images.numpy().squeeze()
W = W.squeeze()
y_man = np.zeros((I_h - k_size + 1, I_w - k_size + 1))
for h in range(I_h - k_size + 1):
    for w in range(I_w - k_size + 1):
        window = images[h : h + k_size, w : w + k_size]
        y_man[h, w] = np.sum(window * W.detach().numpy()) + B

print("Y(Manual): \n", y_man)
```

<pre>
Y(Pytorch) : 
 [[-0.6482204  -0.4697213  -0.72254604]
 [-0.50705934 -0.38746536 -0.48394796]
 [-0.15853219 -0.5524138  -0.60327333]]
Y(Manual): 
 [[-0.64822042 -0.46972129 -0.7225461 ]
 [-0.50705934 -0.38746539 -0.4839479 ]
 [-0.15853217 -0.55241382 -0.60327339]]
</pre>
### Shapes of Filters



```python
import torch

N, I_h, I_w, C_i = 32, 28, 26, 3
n_filter = 5
k_size = 3

images = torch.rand(N, C_i, I_h, I_w)
conv = torch.nn.Conv2d(C_i, n_filter, kernel_size = k_size)

y = conv(images)

W = conv.weight
B = conv.bias

print("Input image : {}".format(images.detach().numpy().shape))
print("W / B : {} / {}".format(W.detach().numpy().shape, B.detach().numpy().shape))
print("Output image : {}".format(y.detach().numpy().shape))
```

<pre>
Input image : (32, 3, 28, 26)
W / B : (5, 3, 3, 3) / (5,)
Output image : (32, 5, 26, 24)
</pre>
### Conv Layers with Activation Functions



```python
import numpy as np
import torch

N, I_h, I_w, C_i = 1, 5, 5, 3
n_filter = 3
k_size = 4

images = torch.rand(N, C_i, I_h, I_w)

# Forward Propagation (Pytorch)
conv = torch.nn.Conv2d(C_i, n_filter, kernel_size = k_size)
sigmoid = torch.nn.Sigmoid()
y = conv(images)
y = sigmoid(y)
y = y.detach().numpy().squeeze()
print("Y(Pytorch) : \n", y)

W = conv.weight
B = conv.bias

# Forward Propagation (Manual)
images = images.numpy().squeeze()
y_man = np.zeros((n_filter, I_h - k_size + 1, I_w - k_size + 1))

for c in range(n_filter):
    c_W = W[c, :, :, :]
    c_b = B[c]
    for h in range(I_h - k_size + 1):
        for w in range(I_w - k_size + 1):
            window = images[:, h : h + k_size, w : w + k_size]
            conv = np.sum(window * c_W.detach().numpy()) + c_b.detach().numpy()
            conv = 1 / (1 + np.exp(-conv))
            
            y_man[c, h, w] = conv

print("Y(Manual): \n", y_man)
```

<pre>
Y(Pytorch) : 
 [[[0.44595766 0.4009004 ]
  [0.36888936 0.41369557]]

 [[0.5639003  0.57518417]
  [0.48839545 0.49236757]]

 [[0.5087737  0.5014534 ]
  [0.4796335  0.49631336]]]
Y(Manual): 
 [[[0.44595766 0.40090035]
  [0.36888932 0.41369559]]

 [[0.5639003  0.57518422]
  [0.48839545 0.49236754]]

 [[0.50877369 0.50145337]
  [0.47963357 0.49631336]]]
</pre>
### Models with Sequential Method



```python
import torch

n_neurons = [10, 20, 30]

model = torch.nn.Sequential()
model.add_module('conv1',torch.nn.Conv2d(3, n_neurons[0],  kernel_size = 3))
model.add_module('relu1', torch.nn.ReLU())
model.add_module('conv2',torch.nn.Conv2d(n_neurons[0], n_neurons[1], kernel_size = 3))
model.add_module('relu2',torch.nn.ReLU())
model.add_module('conv3',torch.nn.Conv2d(n_neurons[1], n_neurons[2], kernel_size = 3))
model.add_module('relu3',torch.nn.ReLU())

x = torch.randn(32, 3, 28, 298)
predictions = model(x)

for layer in range(0, len(model), 2):
    W = model[layer].weight
    B = model[layer].bias
    print(W.detach().numpy().shape, B.detach().numpy().shape)
    
print('======')

parameters = model.parameters()
for param in parameters:
    print(param.shape)
```

<pre>
(10, 3, 3, 3) (10,)
(20, 10, 3, 3) (20,)
(30, 20, 3, 3) (30,)
======
torch.Size([10, 3, 3, 3])
torch.Size([10])
torch.Size([20, 10, 3, 3])
torch.Size([20])
torch.Size([30, 20, 3, 3])
torch.Size([30])
</pre>
### Models with Model Sub-classing



```python
import torch

n_neurons = [3, 10, 20, 30]

class TestModel(torch.nn.Module):
    def __init__(self):
        super(TestModel, self).__init__()
        global n_neurons
        
        self.conv_layers = []
        for i in range(0, len(n_neurons) - 1):
            self.conv_layers.append(torch.nn.Conv2d(n_neurons[i], n_neurons[i + 1], kernel_size = 3))
            self.conv_layers.append(torch.nn.ReLU())
            
    def forward(self, x):
        for conv_layer in self.conv_layers:
            x = conv_layer(x)
        return x
        
model = TestModel()
x = torch.randn(32, 3, 28, 28)
predictions = model(x)

print(f"Input: {x.detach().numpy().shape}")
print(f"Output: {predictions.detach().numpy().shape}")

for layer in range(0, len(model.conv_layers), 2):
    W = model.conv_layers[layer].weight
    B = model.conv_layers[layer].bias
    print(W.detach().numpy().shape, B.detach().numpy().shape)
```

<pre>
Input: (32, 3, 28, 28)
Output: (32, 30, 22, 22)
(10, 3, 3, 3) (10,)
(20, 10, 3, 3) (20,)
(30, 20, 3, 3) (30,)
</pre>