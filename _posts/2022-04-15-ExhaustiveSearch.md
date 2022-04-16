---
layout: single
title : "완전검색알고리즘"
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



이 글은 [삼성 SW Expert Academy](https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDN86AAXw5UW6)의 강의 중 중요하다고 생각하는 부분의 요약과 관련 문제의 연습 풀이로 구성되었습니다.

<br>


# 완전검색 알고리즘


Exhaustive Search, Brute Force, Generate and Test algorithm 이라고도 한다.


**모든 경우의 수를 테스트하고 최종 해를 도출하는 방법이다.**


- 경우의 수가 상대적으로 작을때 유용하다.

- 수행속도는 느리지만, 해답을 찾아낼 확률이 높다.

대략 천만번 이하의 연산이 필요한 경우 완전검색을 사용해도 좋은 것 같다.


## 백준


### [2798](https://www.acmicpc.net/problem/2798)



```python
N, M = map(int, input().split())
cards = list(map(int, input().split()))

M_sum_diff_min = 300000 # 차이 초기화
optimal_sum = None # 최적해 초기화

for i in range(0, len(cards)):
    for j in range(i + 1, len(cards)): # 선택된 i번째를 제외하고 그다음부터 끝까지
        for k in range(j+1, len(cards)): # 선택된 i, j 번째를 제외하고 그 다음부터 끝까지
            three_cards = [cards[i], cards[j], cards[k]]
            _sum = sum(three_cards)
            if M >= _sum: # 합이 M을 넘지 않는경우
                M_sum_diff = M - _sum
                if M_sum_diff_min > M_sum_diff: # 차이의 최솟값과 비교해서 더 작은경우
                    M_sum_diff_min = M_sum_diff # 최솟값 갱신
                    optimal_sum = _sum # 최적해 갱신

if optimal_sum is not None:
    print(optimal_sum)            
```

<pre>
5 21
5 6 7 8 9
21
</pre>
### [2231](https://www.acmicpc.net/problem/2231)



```python
N = input()

def calc_decomp_sum(N: str) -> str: # 분해합 계산 함수
    decomp_sum = int(N)
    for digit in N:
        decomp_sum += int(digit)
    return str(decomp_sum)

generators = {} # 분해합(key: str) : 생성자(value: list[int]) 딕셔너리 초기화
N_decomp_sum = calc_decomp_sum(N)
for i in range(1, int(N_decomp_sum)): # 분해합 > 생성자이므로, 1부터 분해합까지 순회
    decomp_sum = calc_decomp_sum(str(i)) # 생성자 i의 분해합 계산
    if generators.get(decomp_sum) is not None: # 분해합에 대한 생성자 i 추가
        generators[decomp_sum].append(i)
    else:
        generators[decomp_sum] = [i]

if generators.get(N) is None: # 생성자가 없는 경우
    print(0)
else:
    generators_list = list(map(int,generators[N])) # 자연수 N에 대한 생성자 조회
    print(min(generators_list)) # 최솟값 출력
```

<pre>
216
198
</pre>
### [7568](https://www.acmicpc.net/problem/7568)



```python
N = int(input())

weights, heights, counts = [], [], [] # input 자료 입력
for case in range(N):
    weight, height = map(int, input().split())
    weights.append(weight)
    heights.append(height)
    
for weight, height in zip(weights, heights): # 각 사람마다 덩치 등수 계산 후 counts에 저장
    count = 0
    for i in range(len(weights)):
        if weight < weights[i] and height < heights[i]: 
            count += 1
    counts.append(count + 1)
    
for count in counts: # 덩치 등수 출력
    print(count, end = ' ')
```

<pre>
5
55 185
58 183
88 186
60 175
46 155
2 2 1 2 5 
</pre>
### [1018](https://www.acmicpc.net/problem/1018)



```python
N, M = map(int, input().split())

board = [] # board input 저장
for n in range(N):
    board.append(input())
    
white_chess = ['WB' * 4 if i % 2 == 0 else 'BW' * 4 for i in range(8)]
black_chess = ['BW' * 4 if i % 2 == 0 else 'WB' * 4 for i in range(8)]
    
white_chess_counts = []
black_chess_counts = []
for width_ind in range(M-8+1):
    for height_ind in range(N-8+1):
        chess = board[height_ind:height_ind+9] # 높이 cut
        chess = [row[width_ind:width_ind+9] for row in chess] # 너비 cut
        
        white_chess_count = 0 # 흰색, 검정색 다시 칠해야 하는 갯수 count
        black_chess_count = 0
        for h in range(8):
            white_chess_count += sum([1 if chess[h][w] != white_chess[h][w] else 0 for w in range(8)])
            black_chess_count += sum([1 if chess[h][w] != black_chess[h][w] else 0 for w in range(8)])
        white_chess_counts.append(white_chess_count)
        black_chess_counts.append(black_chess_count)
        
white_chess_counts.extend(black_chess_counts)
print(min(white_chess_counts)) # 최솟값 출력
```

<pre>
10 13
BBBBBBBBWBWBW
BBBBBBBBBWBWB
BBBBBBBBWBWBW
BBBBBBBBBWBWB
BBBBBBBBWBWBW
BBBBBBBBBWBWB
BBBBBBBBWBWBW
BBBBBBBBBWBWB
WWWWWWWWWWBWB
WWWWWWWWWWBWB
12
</pre>
### [1436](https://www.acmicpc.net/problem/1436)



```python
N = int(input())

def is_eternal(number: int) -> bool: # 종말의 숫자를 확인하는 함수 정의
    number = str(number)
    flag = False
    for i in range(len(number) - 2):
        if number[i:i+3] == '666':
            return True
    return flag

eternal_numbers = [] # 첫번째 종말의 숫자(666)부터 1씩 증가시키며, 종말의 숫자인지 확인 후 저장
number = 666
while True:
    if is_eternal(number):
        eternal_numbers.append(number)
    if len(eternal_numbers) == N: # N개가 쌓이면 반복을 멈추고 가장 마지막 원소 출력
        break
    number += 1

print(eternal_numbers[-1])
```

<pre>
500
166699
</pre>