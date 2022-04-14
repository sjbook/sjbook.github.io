---
layout: single
title : "[백준] 1.입출력과 사칙연산"
author_profile: true
categories: coding_test
tag: [coding test, baekjoon] 
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


# 백준 1단계, 입출력과 사칙연산


## [2557](https://www.acmicpc.net/problem/2557)



```python
print("Hellow World!")
```

<pre>
Hellow World!
</pre>
## [10718](https://www.acmicpc.net/problem/10718)



```python
for i in range(0, 2):
    print("강한친구 대한육군")
```

<pre>
강한친구 대한육군
강한친구 대한육군
</pre>
## [10171](https://www.acmicpc.net/problem/10171)



```python
print("\\    /\\")
print(" )  ( ')")
print("(  /  )")
print(" \\(__)|")
```

<pre>
\    /\
 )  ( ')
(  /  )
 \(__)|
</pre>
## [10172](https://www.acmicpc.net/problem/10172)



```python
print("|\\_/|")
print("|q p|   /}")
print('( 0 )"""\\')
print('|"^"`    |')
print("||_/=\\\\__|")
```

<pre>
|\_/|
|q p|   /}
( 0 )"""\
|"^"`    |
||_/=\\__|
</pre>
## [1000](https://www.acmicpc.net/problem/1000)



```python
_input = input().split()
_input = [int(i) for i in _input] # casting (str -> int)
print(sum(_input))
```

<pre>
1 2
3
</pre>
## [1001](https://www.acmicpc.net/problem/1001)



```python
_input = input().split()
_input = [int(i) for i in _input] # casting (str -> int)
print(_input[0] - _input[1])
```

<pre>
3 2
1
</pre>
## [10998](https://www.acmicpc.net/problem/10998)



```python
_input = input().split()
_input = [int(i) for i in _input] # casting (str -> int)
print(_input[0] * _input[1])
```

<pre>
1 2
2
</pre>
## [1008](https://www.acmicpc.net/problem/1008)



```python
_input = input().split()
_input = [int(i) for i in _input] # casting (str -> int)
print(_input[0] / _input[1])
```

<pre>
1 3
0.3333333333333333
</pre>
## [10869](https://www.acmicpc.net/problem/10869)



```python
_input = input().split()
_input = [int(i) for i in _input] # casting (str -> int)
print(_input[0] + _input[1])
print(_input[0] - _input[1])
print(_input[0] * _input[1])
print(_input[0] // _input[1])
print(_input[0] % _input[1])
```

<pre>
7 3
10
4
21
2
1
</pre>
## [10926](https://www.acmicpc.net/problem/10926)



```python
_id = input()
print(_id + "??!")
```

<pre>
joonas
joonas??!
</pre>
## [18108](https://www.acmicpc.net/problem/18108)



```python
year = input()
print(int(year) - 543)
```

<pre>
2541
1998
</pre>
## [10430](https://www.acmicpc.net/problem/10430)



```python
_input = input().split()
_input = [int(i) for i in _input] # casting (str -> int)
a, b, c = _input
print((a + b) % c)
print(((a % c) + (b % c)) % c)
print((a * b) % c)
print(((a % c) * (b % c)) % c)
```

<pre>
5 8 4
1
1
0
0
</pre>
## [2588](https://www.acmicpc.net/problem/2588)



```python
three_digit_natural_number1 = int(input())
three_digit_natural_number2 = input()

multiplication_factors = [int(d) for d in three_digit_natural_number2[::-1]] # reverse, casting (str -> int)

for digit in range(0, len(multiplication_factors)):
    print(three_digit_natural_number1 * multiplication_factors[digit])

print(three_digit_natural_number1 * int(three_digit_natural_number2))
```

<pre>
472
385
2360
3776
1416
181720
</pre>