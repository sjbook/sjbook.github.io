---
layout: single
title : "[백준] 7.기초수학1"
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


# 기본수학 1


## [1712](https://www.acmicpc.net/problem/1712)



```python
A, B, C = map(int, input().split()) # A: 고정비용, B: 가변비용, C: 노트북 가격
count = 0

if B >= C:
    print(-1)
else:
    break_point = A/ (C-B)
    if break_point % 1 == .0:
        print(int(break_point) + 1)
    elif break_point % 1 < 0.5:
        print(int(round(break_point + 0.5, 0)))
    else:
        print(int(round(break_point, 0)))
```

<pre>
2100000000 9 10
2100000001
</pre>
\\(수익 > 전체비용\\) 이려면,

\\(수익 - 전체비용 > 0\\) 이어야한다.

즉, \\(count(C - B) - A\\)이며

\\(count > A/(C-B)\\)이다.

즉, \\(손익분기점 (break point) = A/(C-B)\\)이다.



여기서, 

\\(C > B\\) 라면, \\(A > 0\\)으로 가능하지만, 

\\(C = B\\) 이면 분모가 0이되므로 불가능하고,

\\(C < B\\) 라면, \\(A < 0\\) 이되므로 또한 불가능하다.



다만  \\(A/(C-B)\\)는 소수가 될 수 있으므로, 정수형으로 고치고 올림을 해서 답해야 한다.


## [2292](https://www.acmicpc.net/problem/2292)



```python
N = int(input())

def a_n(n: int):
    return 3 * n ** 2 - 9 * n + 8

if N == 1:
    print(1)
else:
    n = 2
    while a_n(n) <= N:
        n += 1
    print(n - 1)
```

<pre>
1
1
</pre>
벌집에서 숫자들을 감싸고 있는 층으로 그룹을 묶을 수 있다.

1(중앙, 1층) => 2 ~ 7(2층) => 8 ~ 19(3층) => 20 ~ 37(4층) ... 순이다.

이때, 같은 그룹에 속하는 숫자라면 지나는 방의 수도 같다.

예를 들어, 1에서 출발하여 13까지 3개의 방을 지나면 된다.

1에서 출발하여 19까지 가는경우에도 역시 3개의 방을 지나면 된다.

**그렇다면 문제는 N이 어떤 숫자 그룹에 속하는지 찾으면 된다.**



수열의 규칙을 찾기 위해, 각 숫자의 초항만을 살펴보면,

1 => 2 => 8 => 20 => 38으로 

n >= 2 에서 \\(a_{n+1} - a_{n} = 6(n-1)\\)임을 알 수 있다.

점화식을 풀면, \\(a_{n} = \sum_{i=1}^{n-1}6(i-1) + 2\\)이며,

덧셈기호(시그마)를 풀고 n >= 2에서만 가능하다는 것을 고려하면, \\(a_{n} = 3n^2 - 9n + 8\\)이다.

**따라서 a_{n}을 여러개 만들어가며, 주어진 숫자가 n이 몇일때에 속하는지 판단하면 된다.**


## [1193](https://www.acmicpc.net/problem/1193)



```python
X = int(input())

def a_n(n: int):
    return 1/2*n**2 - 1/2*n + 1

n = 1 # n = 분모 + 분자
while a_n(n) <= X:
    n += 1
if n % 2 == 1:
    denom = (1) + (X - a_n(n-1))
    numer = (n-1) - (X - a_n(n-1))
else:
    denom = (n-1) - (X - a_n(n-1))
    numer = (1) + (X - a_n(n-1))
    
print(f'{int(denom)}/{int(numer)}')
```

<pre>
14
2 / 4
</pre>
분자와 분모를 합했을때, 합이 일정한 것으로 숫자의 그룹을 묶을 수 있다.

예를 들면, 1/2 와 2/1은 분모와 분자를 합했을때, 3이므로 하나의 그룹이다.

이처럼 그룹을 먼저 찾고, 그 안에서 하나씩 찾으면 시간을 훨씬 절약할 수 있을 것이다.

그룹의 초항을 살펴 보면, 1 => 2 => 4 => 7 => 11으로 \\(a_{n+1} - a_{n} = n\\)임을 알 수 있다.



점화식을 풀면, \\(a_{n} = \sum_{i=1}^{n-1}i + 1\\)이며, \\(a_{n} = 1/2n^2 - 1/2n + 1\\)이다.

문제는 X가 어떤 그룹에 속하는지 찾은 후, 남은 반복(X - a_n(n-1))을 동안 분자에 1을 더하고, 분모에 1을 빼는 식으로 분수를 구하면 된다.

분모 + 분자가 홀수인경우는, 1/N으로 시작한다.

짝수인 경우는, N/1로 시작한다.


## [2869](https://www.acmicpc.net/problem/2869)



```python
A, B, V = map(int, input().split())
D = (V-B)/(A-B)
if D % 1 == .0:
    D = int(D)
elif D % 1 < 0.5:
    D = int(round(D + 0.5, 0))
else:
    D = int(round(D, 0))
print(D)
```

<pre>
100 99 1000000000
999999901
</pre>
달팽이는 하루에 A - B 만큼 올라간다. 

그러나 정상에서는 미끄러 지지 않으므로, 마지막 날에는 낮에 올라가고 밤에 미끄러지지 않고 종료될 것이다.

따라서 \\(V-B <= (A-B)D\\)가 되는 D를 찾아서 1을 더하면 된다.

식을 정리하면, \\({V-B \over A-B} <= D\\)이며

\\({V-B \over A-B}\\)는 소수가 될 수 있으므로, 올림처리한다.


## [10250](https://www.acmicpc.net/problem/10250)



```python
T = int(input())

def find_room(H : int, W : int, N: int) -> int:
    Y = N % H 
    XX = N // H
    XX = str(XX + 1)
    
    if Y == 0: # 나머지가 0인경우는 H로 대입, 나눈 몫은 1을 뺴야함
        Y = H
        XX = str(int(XX) - 1)
    
    if len(XX) < 2: # 1인경우 01로 고침
        XX = '0' + XX
    
    ho = str(Y) + XX
    return int(ho)

for t in range(0, T):
    H, W, N = map(int, input().split())
    print(find_room(H, W, N))
```

<pre>
2
6 12 10
402
30 50 72
1203
</pre>
101, 201, 301 부터 차례로 손님을 배정하면 된다.

층수는 최대 H 층 까지 이므로, H가 넘어가는 N에 대해서는 X01호에 배정할 수 없고, 그 옆칸인 X02호에 배정해야 한다.

이런식이라면 층수는 N을 H로 나눈 나머지가 되고, 호수는 N을 H로 나눈 몫에 1을 더한 값이 된다.

나머지가 0인경우는 층수를 나눈 숫자로 고쳐주고, 호수도 고쳐야한다.


## [2775](https://www.acmicpc.net/problem/2775)



```python
def search_number_people(a : int, b : int, number_people_list: list[int]) -> int:
    item = number_people_list[a][b - 1]
    if item != 0:
        return item
    else:
        number_people = 0
        if a == 0:
            number_people_list[a][b-1] = b
            return b
        else:
            for ho in range(1, b + 1):
                number_people += search_number_people(a-1, ho, number_people_list)
            number_people_list[a][b-1] = number_people
            return number_people
        

T = int(input())
for t in range(0, T):
    k = int(input())
    n = int(input())
    number_people_list = [[0] * n for _ in range(0, k + 1)]
    print(search_number_people(k, n, number_people_list))
```

<pre>
2
1
3
6
2
3
10
</pre>
이중리스트 초기화 방법



```python
c = [[0] * 3 for _ in range(0, 3)]
c[1][1] = 1
print(c)
```

<pre>
[[0, 0, 0], [0, 1, 0], [0, 0, 0]]
</pre>
재귀 함수를 사용하는경우, 했던 계산을 다시해야하는 경우가 생긴다. 이런경우에는 동적 프로그래밍을 통해 해결한다.

여러 방법이 있겠지만, 한가지 방법은 계산을 하고, 그 내용을 저장해 두는 것이다.

그리고 저장해둔 리스트를 조회하고 있다면 가져오고, 없다면 계산하는 식으로 프로그램을 짠다.

이러한 간단한 방식으로도 상당한 계산양을 줄일 수 있다.


## [2839](https://www.acmicpc.net/problem/2839)



```python
N = int(input())
div3 = 0
div5 = 0
n = N
while n > 0:
    if n % 5 == 0:
        div5 += n // 5
        break
    else:
        n -= 3
        div3 += 1
if n < 0:
    print(-1)
else:
    print(div5 + div3)
```

<pre>
11
3
</pre>
5의 배수가 될때까지 3을 빼는 방식


## [10757](https://www.acmicpc.net/problem/10757)



```python
A, B = map(int, input().split())

print(A + B)
```

<pre>
9223372036854775807 9223372036854775808
18446744073709551615
</pre>
파이썬은 오버플로가 일어나지 않는 것 같다..?

일반적인 경우 덧셈하는 역할을 직접 수행하는 것 같다.






```python
A, B = input().split()

def add(A: str, B: str, carry: str) -> str:
    _sum = int(A) + int(B) + int(carry)
    return (str(_sum // 10), str(_sum % 10))

if len(A) >= len(B):
    target = A
    target2 = '0'*(len(A) - len(B))+ B
else:
    target = B
    target2 = '0'*(len(B) - len(A))+ A
    
carry = '0'
result = ''
for d in range(len(target) - 1, -1, -1):
    carry, _sum= add(target[d], target2[d], carry)
    result += _sum
    if d == 0 and carry != '0':
        result += carry
    
print(result[::-1])
```

<pre>
1 13
14
</pre>