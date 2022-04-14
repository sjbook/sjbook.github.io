---
layout: single
title : "헷갈리는 python 기본"
author_profile: true
categories: python
tag: [python]
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


# python 공부


## 연산자 축약


a = a - 4 는 a -= 4 로 축약하여 쓸 수 있다.



```python
a = 5
a = a - 4
print(a)
```

<pre>
1
</pre>

```python
a = 5
a -= 4
print(a)
```

<pre>
1
</pre>
이와 비슷하게 -=, +=, \*=, \*\*= 등으로 축약하여 사용할 수 있다.



```python
a = 5
a = a ** 2
print(a)
```

<pre>
25
</pre>

```python
a = 5
a **= 2
print(a)
```

<pre>
25
</pre>
## slicing


파이썬은 slicing 이라는 기능을 제공하는데, 다음과 같은 형태로 인덱스를 제공하여 사용할 수 있다.



 - **start:end:increment**



index는 0부터 시작하며, end로 넘겨준 값은 포함하지 않는다.

increment는 생략하면 default = 1이다.



```python
a = '123456789'
print(a[1:5])
```

<pre>
2345
</pre>
처음부터 slicing하고 싶은 경우에는 : 앞을 생략한다



```python
print(a[:5])
```

<pre>
12345
</pre>
마찬가지로 마지막까지 slicing하고 싶은 경우에는 : 뒤를 생략한다.



```python
print(a[1:])
```

<pre>
23456789
</pre>
increment를 활용하여 3칸씩 건너뛸 수도 있다.



```python
print(a[::3])
```

<pre>
147
</pre>
## docstring 단축키


jupyter notebook 활용시, docstring을 보고 싶은 함수위에 커서를 두고 shitf + tab을 입력하면 docstring을 확인할 수 있다.



```python
a.join()
```

그외에도 편리한 단축키 모음은 Help -> Keyboard shortcuts 에서 확인할 수 있다.


## in 연산


리스트 안에 내가 원하는 값이 들어있는지 확인하고 싶은 경우가 있다.



그런 경우 **value in list** 형태로 간단히 확인할 수 있다.



```python
a = [1, 5, 8, 11, 16, 17]
print(16 in a)
```

<pre>
True
</pre>
딕셔너리에도 같은 방법을 적용할 수 있는데, 이 방법으로 내가 원하는 key가 dictionary에 있는지 확인할 수 있다.



```python
a = {'key1' : 'value1', 'key2' : 'value2'}
print('key3' in a)
```

<pre>
False
</pre>
이 방법으로 value는 확인할 수 없다.



```python
a = {'key1' : 'value1', 'key2' : 'value2'}
print('value1' in a)
```

<pre>
False
</pre>
## tuple unpacking


튜플은 튜플의 값을 차례대로 변수에 대입할 수 있는 tuple unpacking을 지원한다.



```python
a = (4, 8, 46)
b, c, d = a
print(b, c, d)
```

<pre>
4 8 46
</pre>
이것을 잘 활용하면, 하나의 함수에서 복수개의 리턴값을 받을 수 있다.



```python
def add_3_5_6(_input):
    return (_input + 3, _input + 5, _input + 6)
e, f, g = add_3_5_6(3)
print(e, f, g)
```

<pre>
6 8 9
</pre>
## dictionary 자료형


python의 dictionary는 인덱스가 없으므로 순서를 따지지 않는다. 

대신 key가 존재한다.



```python
a = {'key1' : 'value1', 'key2' : 'value2'}
print(a['key1'])
```

<pre>
value1
</pre>
### 추가


새로운 key와 value 쌍을 추가 하고 싶으면, 다음과 같이 입력한다.



**a['새로운 키'] = 새로운 value**



```python
a['key3'] = 'value3'
print(a)
```

<pre>
{'key1': 'value1', 'key2': 'value2', 'key3': 'value3'}
</pre>
### 업데이트


하나의 key에 대해 다른 value가 들어오면, 그 value로 업데이트 된다.



```python
a['key1'] = 'value3'
print(a['key1'])
```

<pre>
value3
</pre>
딕셔너리의 update 메서드는 두개의 딕셔너리를 병합한다.

이 때, 겹치는 키가 있다면, parameter로 넘겨진 값으로 덮어씌워진다.



```python
print(a)
b = {'key1' : 'value1', 'key4' : 'value4'}
print(b)
```

<pre>
{'key1': 'value3', 'key2': 'value2', 'key3': 'value3'}
{'key1': 'value1', 'key4': 'value4'}
</pre>

```python
a.update(b)
print(a)
```

<pre>
{'key1': 'value1', 'key2': 'value2', 'key3': 'value3', 'key4': 'value4'}
</pre>
### 초기화


clear 메서드로 초기화 할 수 있다.



```python
a.clear()
print(a)
```

<pre>
{}
</pre>
### 존재하지 않는 key 접근


존재하지 않는 key에 대해 접근하면, dict['key']를 통한 접근은 KeyError가 발생한다.



```python
b['key5']
```

그러나 get함수를 통한 접근은 None을 리턴하므로, 프로그램이 중간에 오류로 인해 멈추지 않는다.



```python
print(b.get('key5'))
```

<pre>
None
</pre>
## boolean


python도 다른 프로그램과 같이 0은 False, 0이 아닌 값은 True로 인식한다.



그러나 특이한점은 None 또는 비어있는 자료형도 False로 활용할 수 있고, 값이 들어있는 자료형은 True로 활용할 수 있다.



```python
0 == False
```

<pre>
True
</pre>

```python
if None:
    print('True')
```


```python
if '':
    print('True')
```


```python
if []:
    print('True')
```


```python
if 'istrue?':
    print('True')
```

<pre>
True
</pre>

```python
if {'key1' : 'value1'}:
    print('True')
```

<pre>
True
</pre>
파이썬은 if, elif, else 로 조건문을 활용한다.



```python
a = 4
if a == 3:
    print('a = 3')
elif a == 5:
    print('a = 5')
elif a == 6:
    print('a = 6')
else:
    print('the others')
```

<pre>
the others
</pre>
## 반복문


### break


break 는 반복문안에서 loop block을 종료하고, 다음코드로 넘어가게 한다.



따라서 무한루프를 주고, 조건에 따라 종료시킬때 사용될 수 있다.



```python
for i in range(0, 10):
    print(i)
    if i == 5:
        break
        
print('end')
```

<pre>
0
1
2
3
4
5
end
</pre>

```python
i = 0
while True:
    print(i)
    i += 1
    if i == 6:
        break

print('end')
```

<pre>
0
1
2
3
4
5
end
</pre>
### continue


continue는 점프하는 역할을 한다.



반복문을 끝내지는 않고, 다음 루프로 넘어갈 수 있게 한다.



```python
for i in range(0, 10):
    if i % 2 ==0:
        print(i)
    else:
        continue
        
print('end')
```

<pre>
0
2
4
6
8
end
</pre>
### enumerate


반복문에서 index와 값 모두를 사용하고 싶은 경우 enumerate를 사용하면 편리하다.



```python
a = [11, 15, 14, 8, 2, 4 ,9]
for i, value in enumerate(a):
    print(i, value)
```

<pre>
0 11
1 15
2 14
3 8
4 2
5 4
6 9
</pre>
### range


range()와 같은 generator를 활용하면, 원하는 list를 쉽게 만들 수 있다.



```python
a = list(range(1, 100, 4))
print(a)
```

<pre>
[1, 5, 9, 13, 17, 21, 25, 29, 33, 37, 41, 45, 49, 53, 57, 61, 65, 69, 73, 77, 81, 85, 89, 93, 97]
</pre>
## 함수


### parameter


파라미터에 기본값을 줄 수 있다.



```python
def add(input1, input2 , input3 = 3):
    return input1 + input2 + input3

print(add(1, 2, 3))
print(add(1, 2))
```

<pre>
6
6
</pre>
그러나 default parameter 뒤에 일반 파라미터가 올 수는 없다.



```python
def add(input1, input2 = 3, input3):
    return input1 + input2 + input3

print(add(1, 2, 3))
print(add(1, 2))
```

### return


함수에 return 만 있거나, return이 없는 경우에는 None을 반환한다.



```python
def add(input1, input2, input3 = 3):
    input1 + input2 + input3

print(add(1, 2, 3))
```

<pre>
None
</pre>

```python
def add(input1, input2, input3 = 3):
    input1 + input2 + input3
    return

print(add(1, 2, 3))
```

<pre>
None
</pre>
### 가변길이 인자


#### args


전달되는 파라미터의 개수가 가변적인경우에는 가변길이 인자(args, kwargs)를 활용할 수 있다.



args는 튜플 형태로 전달되며, 함수의 head 부분에는 \*변수명으로 전달한다.



```python
def add(*args):
    return sum(args)

print(add(1, 2))
print(add(1, 2, 3, 4, 5, 6, 7))
```

<pre>
3
28
</pre>
#### kwargs


kwargs는 딕셔너리 형태로 전달되며, 함수의 head부분에는 **변수명으로 전달한다.



함수에 argument를 전달할때는 파라미터의 이름과 값을 함께 전달한다.



```python
def print_kwargs(**kwargs):
    print(kwargs)

print_kwargs(one = 1, two = 2, three = 3)
```

<pre>
{'one': 1, 'two': 2, 'three': 3}
</pre>
## format


format 함수를 활용하여, 문자열에 변수의 값을 전달 할 수 있다.



```python
'오늘의 날씨는 {}도 이며, 강수확률은 {}%입니다.'.format(23, 50)
```

<pre>
'오늘의 날씨는 23도 이며, 강수확률은 50%입니다.'
</pre>
formatting 할 변수의 수가 너무 많아지는 경우 place holder로 이름을 명시할 수 있다.



```python
'오늘의 날씨는 {temp}도 이며, 강수확률은 {prob}%입니다.'.format(temp = 23, prob = 50)
```

<pre>
'오늘의 날씨는 23도 이며, 강수확률은 50%입니다.'
</pre>
## lambda 표현식


간단한 함수를 표현할때, def로 정의하지 않고, lambda 표현식으로 간결하게 함수를 사용할 수 있다.



```python
(lambda x: x**2)(2)
```

<pre>
4
</pre>
함수의 인수로 2개 이상도 받을 수 있다.



```python
(lambda x, y : x+y)(3, 4)
```

<pre>
7
</pre>
list의 sort함수는 key로 함수를 받는데, lambda가 유용하게 사용될 수 있다.



```python
a = ['5hong', '1bong', '2woong']
a.sort(key = lambda x: int(x[0]))
print(a)
```

<pre>
['1bong', '2woong', '5hong']
</pre>
## filter, map


filter(함수, 리스트) 형식으로 사용하며 조건에 맞는 element만 남겨준다.



이때, 함수는 true, false를 반환하는 함수이다.



```python
b = filter(lambda x : int(x[0]) % 2 == 0, a)
print(list(b))
```

<pre>
['2woong']
</pre>
map(함수, 리스트) 형식으로 사용하며, 모든 element에 같은 연산을 적용한다.



list comprehension 처럼 사용할 수 있다.



```python
a = [1, 3, 5, 7, 9]
b = map(lambda x: x ** 2, a)
print(list(b))

c = [x ** 2 for x in a]
print(c)
```

<pre>
[1, 9, 25, 49, 81]
[1, 9, 25, 49, 81]
</pre>
## package import


**import package**는 package 모듈 전체를 import 한다.



```python
import math
math.pi
```

<pre>
3.141592653589793
</pre>
**from math import pi**는 math 패키지 안에서 pi 라는 특정한 부분만 import 할 수 있다.



이런 방식으로 import 하면, math.pi가 아닌 pi 로 접근할 수 있다.



```python
from math import pi
pi
```

<pre>
3.141592653589793
</pre>
**from math import \***는 math 모듈 내에 정의된 모든 것을 import 한다.



이 방식은 이름이 중복되어 문제를 일으킬 수 있으므로 권장하지 않는 방법이다.



```python
from math import *
pi
```

<pre>
3.141592653589793
</pre>
**import math as m** 모듈의 별명을 지정하여, math를 m으로서 불러올 수 있다.



이경우 math.pi를 m.pi로 불러올 수 있다.



```python
import math as m
m.pi
```

<pre>
3.141592653589793
</pre>