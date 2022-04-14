---
layout: single
title : "2.DenseLayer"
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


# Dense Layer


각 뉴런들은 서로 다른 weight와 bias를 가진 parametric function으로, filtering 연산으로 볼 수 있다.

따라서 여러개의 뉴런들을 묶은 하나의 층(Dense Layer)는 서로 다른 parametric funciton의 묶음



Filter bank의 개념 : 같은 값을 넣더라도 다른값이 나온다.

​    

Deep Learning : cascaded(layer가 쌓아짐) filter bank 구조



보통 Dense Layer는 모든 노드가 연결된 fully connected layer를 말한다.



network는 edge(connection)와 node로 구성된다.



sigmoid 함수는 파라미터가 없지만, activation layer라고 부르기도 한다.



각 Layer의 출력값은 다음 layer의 input 역할을 한다.


## shape


**Pytorch 기준**



X = (샘플수, 변수개수) 일때,



Weight = (뉴런개수, 변수개수)



Bias = (뉴런개수)



Output = (샘플수, 뉴런개수)


## 실습


### shapes of dense layers



```python
import torch

N, n_feature = 8, 10
X = torch.rand(N, n_feature)

n_neuron = 3
Linear = torch.nn.Linear(in_features = n_feature, out_features = n_neuron)
Sigmoid = torch.nn.Sigmoid()

Y = Sigmoid(Linear(X))

W = Linear.weight
B = Linear.bias


print(f'X: {X.detach().numpy().shape}')
print(f'Weight: {W.detach().numpy().shape}')
print(f'Bias: {B.detach().numpy().shape}')
print(f'y : {Y.detach().numpy().shape}')
```

<pre>
X: (8, 10)
Weight: (3, 10)
Bias: (3,)
y : (8, 3)
</pre>
### shapes of cascaded dense layers



```python
import torch

N, n_feature = 4, 10
X = torch.rand(N, n_feature)

n_neurons = [3, 5]
Linear1 = torch.nn.Linear(in_features = n_feature, out_features = n_neurons[0])
Linear2 = torch.nn.Linear(in_features = n_neurons[0], out_features = n_neurons[1])
Sigmoid = torch.nn.Sigmoid()

# forward propagation
A1 = Sigmoid(Linear1(X))
Y = Sigmoid(Linear2(A1))

# get weight/bias
W1 = Linear1.weight
B1 = Linear1.bias

W2 = Linear2.weight
B2 = Linear2.bias

print(f'X: {X.detach().numpy().shape} \n')

print(f'Weight1: {W1.detach().numpy().shape}')
print(f'Bias1: {B1.detach().numpy().shape}')
print(f'A1: {A1.detach().numpy().shape} \n')

print(f'Weight2 : {W2.detach().numpy().shape}')
print(f'Bias2 : {B2.detach().numpy().shape}')
print(f'Y : {Y.detach().numpy().shape}')
```

<pre>
X: (4, 10) 
Weight1: (3, 10)
Bias1: (3,)
A1: (4, 3) 

Weight2 : (5, 3)
Bias2 : (5,)
Y : (4, 5)
</pre>

### dense layers with python list



```python
import torch

N, n_feature = 4, 10
X = torch.rand(N, n_feature)

n_neurons = [n_feature, 10, 20, 30 ,40, 50 ,60 ,70 ,80 ,90 ,100]

ReLU = torch.nn.ReLU()

dense_layers = []
for i in range(0, len(n_neurons)-1):
    Linear = torch.nn.Linear(in_features = n_neurons[i], out_features = n_neurons[i+1])
    dense_layers.append(Linear)

print(f'Input : {X.detach().numpy().shape}')
for dense_idx, dense in enumerate(dense_layers):
    X = dense(X)
    X = ReLU(X)
    print("After dense layer ", dense_idx)
    print(X.detach().numpy().shape, '\n')

Y = X
```

<pre>
Input : (4, 10)
After dense layer  0
(4, 10) 

After dense layer  1
(4, 20) 

After dense layer  2
(4, 30) 

After dense layer  3
(4, 40) 

After dense layer  4
(4, 50) 

After dense layer  5
(4, 60) 

After dense layer  6
(4, 70) 

After dense layer  7
(4, 80) 

After dense layer  8
(4, 90) 

After dense layer  9
(4, 100) 

</pre>

### Model Implementation with Sequential Method



```python
import torch

n_neurons = [3, 4, 5, 6]

Sigmoid = torch.nn.Sigmoid()

model = []
for i in range(0, len(n_neurons)-1):
    model.append(torch.nn.Linear(n_neurons[i], n_neurons[i+1]))
    model.append(Sigmoid)

model = torch.nn.Sequential(*model)
model
```

<pre>
Sequential(
  (0): Linear(in_features=3, out_features=4, bias=True)
  (1): Sigmoid()
  (2): Linear(in_features=4, out_features=5, bias=True)
  (3): Sigmoid()
  (4): Linear(in_features=5, out_features=6, bias=True)
  (5): Sigmoid()
)
</pre>
### Model implementation with Model-subclassing



```python
import torch

class TestModel(torch.nn.Module):
    def __init__(self):
        super().__init__()
        
        self.dense1 = torch.nn.Linear(n_feature, 10)
        self.dense2 = torch.nn.Linear(10, 20)
        
        self.ReLU = torch.nn.ReLU()
        
    def forward(self, x):
        x = self.dense1(x)
        x = self.ReLU(x)
        x = self.dense2(x)
        x = self.ReLU(x)
        return x
    
model = TestModel()
model
```

<pre>
TestModel(
  (dense1): Linear(in_features=10, out_features=10, bias=True)
  (dense2): Linear(in_features=10, out_features=20, bias=True)
  (ReLU): ReLU()
)
</pre>
### forward propagation of models



```python
import torch

N, n_feature = 4, 10
X = torch.rand(N, n_feature)

class TestModel(torch.nn.Module):
    def __init__(self):
        super().__init__()
        
        self.dense1 = torch.nn.Linear(n_feature, 10)
        self.dense2 = torch.nn.Linear(10, 20)
        
        self.ReLU = torch.nn.ReLU()
        
    def forward(self, x):
        x = self.ReLU(self.dense1(x))
        x = self.ReLU(self.dense2(x))
        return x
    
model = TestModel()
Y = model(X)
```




### Layers in Models



```python
model
```

<pre>
Sequential(
  (0): Linear(in_features=3, out_features=4, bias=True)
  (1): Sigmoid()
  (2): Linear(in_features=4, out_features=5, bias=True)
  (3): Sigmoid()
  (4): Linear(in_features=5, out_features=6, bias=True)
  (5): Sigmoid()
)
</pre>

```python
import torch

n_neurons = [3, 4, 5, 6]

Sigmoid = torch.nn.Sigmoid()

model = []
for i in range(0, len(n_neurons)-1):
    model.append(torch.nn.Linear(n_neurons[i], n_neurons[i+1]))
    model.append(Sigmoid)

model = torch.nn.Sequential(*model)

for i in range(0, len(model), 2):
    W = model[i].weight
    B = model[i].bias
    
    print(W.detach().numpy().shape, B.detach().numpy().shape)
```

<pre>
(4, 3) (4,)
(5, 4) (5,)
(6, 5) (6,)
</pre>
### Trainable Variables in Models



```python
import torch

n_neurons = [3, 4, 5, 6]

Sigmoid = torch.nn.Sigmoid()

model = []
for i in range(0, len(n_neurons)-1):
    model.append(torch.nn.Linear(n_neurons[i], n_neurons[i+1]))
    model.append(Sigmoid)

model = torch.nn.Sequential(*model)

def count_parameters(model):
    return sum(p.numel() for p in model.parameters() if p.requires_grad)

for i in range(0, len(model), 2):
    print(count_parameters(model[i]))
```

<pre>
16
25
36
</pre>