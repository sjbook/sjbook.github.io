---
layout: single
title : "탐욕알고리즘"
author_profile: true
categories: coding_test
tag: [coding test, baekjoon, python] 
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


# Greedy algorithm (탐욕 알고리즘)


매 결정 순간마다 그 순간 최적해를 선택하는 방식으로 최종 해답에 도달하는 방법



선택 순간마다 지역적 최적값이지만 최종해가 최적이라는 보장은 없다.


수행과정



1. 부분 문제의 최적해를 구한 뒤, 부분 해 집합에 추가



2. 새로운 부분해 집합이 실행 가능한지 확인하고, 제약조건을 위반하지 않는지 검사



3. 새로운 부분해 집합이 문제의 해가 되는지 확인



아직 전체 해가 완성되지 않았으면, 해 선택부터 다시 시작


## 백준


### [11047](https://www.acmicpc.net/problem/11047)



```python
N, K = map(int, input().split())

A = []
for i in range(N):
    A.append(int(input()))
coin_counts = [0 for i in range(N)]
    
def choose_coin(K: int, A: list[int]) -> int: # 가장 큰 동전 선택
    coin_ind = 0 
    for i in range(N):
        if K - A[i] < 0:
            return i - 1
        elif i == len(A) - 1:
            return i
        
while True:
    coin_ind = choose_coin(K, A) # 가장 큰 동전 선택
    count, remains = divmod(K, A[coin_ind]) # 몫과 나머지 계산
    coin_counts[coin_ind] = count
    if remains == 0: # 잔돈이 없으면 종료
        break 
    else: # 잔돈이 남으면 재시도
        K = remains

print(sum(coin_counts))    
```

<pre>
10 4790
1
5
10
50
100
500
1000
5000
10000
50000
12
</pre>
### [1931](https://www.acmicpc.net/problem/1931)



```python
N = int(input())

conference_time = []
for i in range(N):
    conference_time.append(list(map(int,input().split())))
    
conference_time.sort(key = lambda x: (x[1], x[0])) # 시작, 종료 시간 기준으로 정렬
  
count = 0
now_time = 0
for start, end in conference_time: 
    if start >= now_time: # 회의 시작시간이 현재시간보다 이후라면 회의 잡음
        count += 1
        now_time = end
        
print(count)
```

<pre>
11
1 4
3 5
0 6
5 7
3 8
5 9
6 10
8 11
8 12
2 13
12 14
4
</pre>
### [11399](https://www.acmicpc.net/problem/11399)



```python
N = int(input())
P = list(map(int, input().split()))

P.sort() # 소요시간 순서대로 정렬 : 가장빠르게 끝낼수 있는 사람부터 처리함
taking_time = [P[i] * (N - i)  for i in range(N)] # 시간 합 구함
print(sum(taking_time))
```

<pre>
5
3 1 4 3 2
32
</pre>
시간의 합을 구하는 부분은 다음과 같이 생각하였다.



시간 순서대로 정렬한 경우, P = [1,2,3,3,4]와 같이 정렬될 수 있다.



이때 1번째 사람은 1분이 필요하며,



이때 2번째 사람은 1 + 2분이 필요하다.



마찬가지로 마지막 사람은 1 + 2 + 3 + 3 + 4분이 필요하다.



즉, 1은 5명 모두가 필요하며,



2는 4명, 4는 1명만 필요하게 된다.



즉, P의 i번째 원소는 N-i 번 중복해서 나타나게 된다.


### [1541](https://www.acmicpc.net/problem/1541)



```python
equation = input()

def plus(number_str: str) -> int:
    numbers_list = number_str.split('+') # '+' 기준으로 분할하여 숫자만 남김
    numbers_list = [int(num) for num in numbers_list] # int 캐스팅
    return sum(numbers_list) # 합계 리턴

equation_list = equation.split(sep = '-') # '-' 기준으로 수식을 쪼갬
equation_list = [plus(eq) for eq in equation_list]

answer = equation_list[0] # 쪼개진 수식 '-' 계산
for i in range(1, len(equation_list)):
    answer -= equation_list[i]
print(answer) 
```

<pre>
0009-0009
0
</pre>
### [13305](https://www.acmicpc.net/problem/13305)



```python
N = int(input())
road_len = list(map(int, input().split()))
oil_price = list(map(int, input().split()))

cost = 0
min_price = oil_price[0] # 최솟값 초기화
for i in range(0, N-1):
    if min_price > oil_price[i]: # 현재 도시가 최솟값보다 더 싸다면, 최솟값 대체
        min_price = oil_price[i]
    cost += min_price * road_len[i] # 도로를 지남
        
print(cost)
```

<pre>
4
2 3 1
5 2 4 1
18
</pre>