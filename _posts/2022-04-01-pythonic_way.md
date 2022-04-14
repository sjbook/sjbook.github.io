---
layout: single
title : "파이썬스러운 방식"
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


# 파이썬 문법


## 들여쓰기(indent)


들여쓰기는 PEP8(Python Enhancement Proposals 8)에 따라 공백(스페이스 바) 4칸을 원칙으로 한다.


코드를 여러 줄에 걸쳐 작성하는 경우에는 공백 4칸 인덴트를 한번 더 추가하여, 다른 행과 구분되게 한다.



```python
a = sum(
    (1, 2),
    (3))
```

## 네이밍 컨벤션


파이썬의 네이밍 컨벤션은 스네이크 케이스(단어와 단어를 \_로 구분)를 따른다.



직접 작성하는 코드는 소문자 변수명과 소문자 함수명을 기본으로 한다.



```python
student_name = 'Juyoung Hong'
```

## 타입 힌트


파이썬은 동적 타이핑 언어이므로 제네릭이 필요 없다.



그렇지만 타입을 명시하지 않으면, 가독성을 낮추고 버그가 발생할 확률이 높아지므로, 타입을 명시 해주는 것이 좋다.



이것은 PEP의 Type Hints를 사용하여 구현할 수 있다.



```python
a: str = "1"
b: list[int] = [1, 2, 3]
c: dict[str, int] = {"key1" : 1, "key2" : 2}
d: tuple[int, str, float] = (1, "Hong", 4.5)
```

위와 같은 형태로 변수의 타입을 선언할 수 있다.



첫 번째 줄의 경우, a라는 변수는 "1" 이라는 값을 갖는 문자열 변수라는 것을 쉽게 알 수 있다.



함수에도 사용할 수 있다.



```python
def iszero(a: int) -> bool:
    return a == 0
```

위의 경우, fn() 이라는 함수는 a라고 하는 argument를 하나 갖고, a라는 argument는 정수형(int)타입이며 함수의 리턴값은 bool로, True 혹은 False를 리턴 할 것이라는 것을 한눈에 쉽게 알 수 있다.


그러나 이러한 type hint는 강제 규약이 아니므로 a: str = 1 과 같은 경우를 주의하여 사용해야 한다.



```python
a: str = 1 # 정수형 타입에 문자열로 힌트를 주어도 에러가 발생하지 않는다.
```

온라인 코딩 테스트와 같은 경우, mypy를 사용하면 타입힌트 오류를 자동으로 확인할 수 있다.


```bash

pip install mypy

```

로 설치 후


```bash

mypy mypythonfile.py

```

로 타입힌트 오류를 검사할 수 있다.


\*.ipynb 파일의 경우, nb-mypy 등을 활용하면 사용할 수 있는 듯 하다.


## list comprehension


리스트 컴프리헨션은 가독성이 높으며, 다방면에 유용하게 사용할 수 있다.



```python
a = []
for n in range(1, 10 + 1):
    if n % 2 == 1:
        a.append(n * 2)
print(a)
```

<pre>
[2, 6, 10, 14, 18]
</pre>
예를 들어 위의 코드는 리스트 컴프리헨션을 활용하면 다음과 같이 축약 할 수 있다.



```python
b = [n*2 for n in range(1, 10+1) if n % 2 == 1]
print(b)
```

<pre>
[2, 6, 10, 14, 18]
</pre>
리스트 뿐만 아니라 딕셔너리에도 사용할 수 있다.



```python
a = {key : value for key, value in enumerate(b)}
print(a)
```

<pre>
{0: 2, 1: 6, 2: 10, 3: 14, 4: 18}
</pre>
대체로 반복문으로 작성하는 것 보다 리스트 컴프리헨션을 활용한 경우 처리 속도도 더 빠른것으로 알고 있다.


그러나 이 역시도 너무 길어 지면 읽기 어려워지므로, 표현식은 대체로 2개를 넘지 않도록 작성한다.


## Generator


제너레이터는 loop의 반복 동작을 제어할 수 있는 루틴 형태이다.



제너레이터를 활용하면, 1억개의 숫자를 메모리 어딘가에 저장하고 있을 필요가 없으며, 제너레이터로 언제든 숫자를 만들 수 있다.


### yield 구문


제너레이터가 중간값을 리턴한다는 의미로, 함수가 종료되지 않고 끝까지 실행된다.



```python
def get_natural_number():
    n = 0
    while True:
        n += 1
        yield n
```

위의 경우 함수의 리턴값은 제너레이터가 된다.



```python
g = get_natural_number()
print(g)
```

<pre>
<generator object get_natural_number at 0x0000020897EDCAC0>
</pre>
다음 값을 생성하려면 next()로 추출하면 되며, 10개의 값을 생성하고 싶은 경우, next()를 10번 수행하면 된다.



```python
for _ in range(0, 10):
    print(next(g))
```

<pre>
1
2
3
4
5
6
7
8
9
10
</pre>
제너레이터는 여러 타입의 값을 하나의 함수에서 생성하는 것도 가능하다.



```python
def generator():
    yield 1
    yield 'string'
    yield True
```


```python
g = generator()
print(next(g))
print(next(g))
print(next(g))
print(next(g))
```

<pre>
1
string
True
</pre>
range는 제너레이터의 방식을 활용한 대표적인 함수로, for 문에서 사용하는 경우 제너레이터의 next()를 호출하듯 매번 다음 숫자를 생성한다.



생성 조건만 정해두고 필요할때 생성해서 꺼내쓰는 방식은 메모리 점유 측면에서 훨씬 효율적이다.



또한 인덱스로 접근하는 경우에도 바로 생성하게끔 되어 있어, 불편없이 사용할 수 있다.



```python
r = range(0, 10000)
print(r[127])
```

<pre>
127
</pre>
## enumerate


여러 자료 형을 인덱스를 포함한 enumerate 객체로 리턴해준다.



**인덱스를 자동으로 부여해 주므로, 인덱스와 값을 함께 출력하는 경우에 매우 편리하다.**



```python
a = [15, 1, 3, 7, 8]
for i, v in enumerate(a):
    print(i, v)
```

<pre>
0 15
1 1
2 3
3 7
4 8
</pre>
## 나눗셈


- '/' -> 타입을 유지하지 않는다. ex) 5/3 = 1.66... (int 형 사이의 나눗셈이지만 float형 자료를 리턴함)

- '/' -> 타입을 유지한다. ex) 5//3 = 1 (int 형 사이의 나눗셈으로 int형 자료를 리턴함, **정수형에서 나눗셈의 몫을 구함**)

- '%' -> 나머지를 구하는 연산

- 몫과 나머지를 동시에 구하는 경우에는 divmod()함수를 활용한다.



```python
quotient, remainder = divmod(5, 3)
print(quotient)
print(remainder)
```

<pre>
1
2
</pre>
## print


리스트를 출력하는 경우에는 ' '.join(a)로 묶어서 처리하면 좋다.



```python
a = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
print(' '.join(a))
```

<pre>
a b c d e f g
</pre>
인덱스에 1을 더해서 원소와 함께 출력하는 경우 formatting을 활용하여 다음과 같이 할 수 있다.



```python
for idx, item in enumerate(a):
    print('{} : {}'.format(idx + 1, item))
```

<pre>
1 : a
2 : b
3 : c
4 : d
5 : e
6 : f
7 : g
</pre>
## f_string


f_string을 활용하면 변수를 뒤에 별도로 부여할 필요 없어 편리하고, 간결하며 직관적이다.



```python
for idx, item in enumerate(a):
    print(f'{idx + 1} : {item}')
```

<pre>
1 : a
2 : b
3 : c
4 : d
5 : e
6 : f
7 : g
</pre>
## pass


코드의 전체 골격을 잡아놓고, 자세한 내용은 나중에 차근차근 생각하고 싶은 경우가 있다.



이러한 경우 pass를 사용한다.



이것은 목업 인터페이스를 구현하고, 자세한 내용은 추후에 구현할 수 있게 한다.



```python
def myfunction():
```


```python
def myfunction():
    pass

m = myfunction()
```

pass를 사용하면, 오류 없이 myfunction이 정의된다.


## locals


로컬 심볼 테이블 딕셔너리를 가져오며, 업데이트도 가능하다.



로컬에 선언된 모든 변수를 조회할 수 있으므로, 디버깅에 많은 도움이 된다.



pprint를 함께 활용하면, 보기 좋게 줄바꿈 처리를 해주므로 가독성이 높다.



```python
import pprint

pprint.pprint(locals())
```

## 코드 작성법


Clean Code, 프로그래밍 수련법, PEP8, 구글의 파이썬 스타일 가이드와 같은 문서들을 참고하여, 되도록 지향점에 맞는 코드를 작성하는 것이 좋다.



```python
def numMatchingSubseq(self, S: str, words : list[str]) -> int:
    pass
```

변수명이 무엇을 의미하는지 이해하기 어려우며, 주석이 없다.



이러한 경우 간단한 주석을 부여하거나 docstring을 작성하는 것이 훨씬 가독성이 높다. 



-> 영어로 주석달기 연습이 필요하다.


### 구글 파이썬 스타일 가이드 일부


- 함수의 기본값으로 가변객체를 사용하지 않아야 한다.



 함수가 객체를 수정하면, 기본값이 변경되기 때문이다.

 

기본값으로 [], {}을 사용하면 안된다.



```python
def myfunction(a, b = []):
    b.append(a)
    print(a)
    print(b)
```


```python
myfunction(1)
```

<pre>
1
[1]
</pre>

```python
myfunction(2)
```

<pre>
2
[1, 2]
</pre>
위와 같이 기본값이 변경되어, 혼란을 줄 수 있다.



이경우 불변객체를 대신 사용하는 것이 좋고, None을 명시적으로 대입하는 것도 좋은 방법이다.



```python
def myfunction(a, b = None):
    b = []
    b.append(a)
    print(a)
    print(b)
```


```python
myfunction(1)
```

<pre>
1
[1]
</pre>

```python
myfunction(2)
```

<pre>
2
[2]
</pre>
- True 혹은 False를 판별해야 하는 경우에는 



if flag != [] 대신 if flag로 충분하다.



```python
flag = True
if flag != False:
    print(flag)
```

<pre>
True
</pre>

```python
if flag:
    print(flag)
```

<pre>
True
</pre>
최대 줄길이는 80자로 한다.

