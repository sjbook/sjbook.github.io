---
layout: single
title : "[백준] 3.반복문"
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


# 3. 반복문


## [2739](https://www.acmicpc.net/problem/2739)



```python
N = int(input())
for i in range(1, 10):
    print(f'{N} * {i} = {N*i}')
```

<pre>
2
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
2 * 5 = 10
2 * 6 = 12
2 * 7 = 14
2 * 8 = 16
2 * 9 = 18
</pre>
## [10950](https://www.acmicpc.net/problem/10950)



```python
T = int(input())
for t in range(0, T):
    A, B = [int(x) for x in input().split()]
    print(A + B)
```

<pre>
5
1 1
2
2 3
5
3 4
7
9 8
17
5 2
7
</pre>
## [8393](https://www.acmicpc.net/problem/8393)



```python
n = int(input())
print(sum(list(range(1, n+1))))
```

<pre>
3
6
</pre>
## [15552](https://www.acmicpc.net/problem/15552)



```python
import sys

T = int(sys.stdin.readline())
for t in range(0, T):
    A, B = [int(x) for x in sys.stdin.readline().split()]
    print(A + B)
```

input()으로 먼저 작성한 뒤 sys.stdin.readline() 함수로 변경해도 무방하다.


## [2741](https://www.acmicpc.net/problem/2741)



```python
N = int(input())
for i in range(1, N + 1):
    print(i)
```

<pre>
5
1
2
3
4
5
</pre>
## [2742](https://www.acmicpc.net/problem/2742)



```python
N = int(input())
for i in range(N, 0, -1):
    print(i)
```

<pre>
5
5
4
3
2
1
</pre>
## [11021](https://www.acmicpc.net/problem/11021)



```python
T = int(input())
for i in range(1, T + 1):
    A, B = [int(x) for x in input().split()]
    print(f'Case #{i}: {A+B}')
```

<pre>
5
1 1
Case #1: 2
2 3
Case #2: 5
3 4
Case #3: 7
9 8
Case #4: 17
5 2
Case #5: 7
</pre>
## [11022](https://www.acmicpc.net/problem/11022)



```python
T = int(input())
for i in range(1, T + 1):
    A, B = [int(x) for x in input().split()]
    print(f'Case #{i}: {A} + {B} = {A+B}')
```

<pre>
5
1 1
Case #1: 1 + 1 = 2
2 3
Case #2: 2 + 3 = 5
3 4
Case #3: 3 + 4 = 7
9 8
Case #4: 9 + 8 = 17
5 2
Case #5: 5 + 2 = 7
</pre>
## [2438](https://www.acmicpc.net/problem/2438)



```python
N = int(input())
for i in range(1, N + 1):
    print('*' * i)
```

<pre>
5
*
**
***
****
*****
</pre>
## [2439](https://www.acmicpc.net/problem/2439)



```python
N = int(input())
for i in range(N, 0, -1):
    blank = ' ' * (i - 1)
    star = '*' * (N - i + 1)
    print(blank + star)
```

<pre>
5
    *
   **
  ***
 ****
*****
</pre>
## [10871](https://www.acmicpc.net/problem/10871)



```python
N, X = [int(x) for x in input().split()]
A = [int(x) for x in input().split()]
A_filtered = list(filter(lambda a: a < X, A))
[print(a, end = ' ')for a in A_filtered]
```

<pre>
10 5
1 10 4 9 2 3 8 5 7 6
1 4 2 3 
</pre>
<pre>
[None, None, None, None]
</pre>
## [10952](https://www.acmicpc.net/problem/10952)



```python
while True:
    A, B = [int(x) for x in input().split()]
    if A == 0 and B == 0:
        break
    else:
        print(A + B)
```

<pre>
1 1
2
2 3
5
3 4
7
9 8
17
5 2
7
0 0
</pre>
## [10951](https://www.acmicpc.net/problem/10951) # EOF



```python
while True:
    try:
        A, B = [int(x) for x in input().split()]
        print(A + B)
    except:
        break
```

언제까지 입력을 받아야 하는지 입력값의 갯수를 알 수 없으므로, End Of File Error를 처리해 주는 try 구문이 필요하다.


## [1110](https://www.acmicpc.net/problem/1110)



```python
N = int(input())
N_org =N
count = 0

while True:
    digit_10 = N // 10
    digit_1 = N % 10
    plus = (digit_10 + digit_1) % 10
    N = digit_1 * 10 + plus
    count += 1
    if N_org == N:
        break

print(count)
```

<pre>
26
4
</pre>