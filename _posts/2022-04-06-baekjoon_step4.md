---
layout: single
title : "[백준] 4.1차원 배열"
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


# 1차원 배열


## [10818](https://www.acmicpc.net/problem/10818)



```python
N = int(input())
integers = [int(x) for x in input().split()]
_max = max(integers)
_min = min(integers)
print(_min, _max)
```

<pre>
5
20 10 35 30 7
7 35
</pre>
## [2562](https://www.acmicpc.net/problem/2562)



```python
n1 = int(input())
n2 = int(input())
n3 = int(input())
n4 = int(input())
n5 = int(input())
n6 = int(input())
n7 = int(input())
n8 = int(input())
n9 = int(input())

integers = [n1, n2, n3, n4, n5, n6, n7, n8, n9]
_max = n1
index = 1
max_index = 1
for n in range(1, len(integers)):
    index += 1
    if _max <= integers[n]:
        _max = integers[n]
        max_index = index
        
print(_max)
print(max_index)
```

<pre>
3
29
38
12
57
74
40
85
61
85
8
</pre>
## [2577](https://www.acmicpc.net/problem/2577)



```python
A = int(input())
B = int(input())
C = int(input())

target = str(A * B * C)
for n in range(0, 10):
    n = str(n)
    counts = [1 for d in target if d == n]
    print(sum(counts))
```

<pre>
150
266
427
3
1
0
2
0
0
0
2
0
0
</pre>
## [3052](https://www.acmicpc.net/problem/3052)



```python
input1 = int(input())
input2 = int(input())
input3 = int(input())
input4 = int(input())
input5 = int(input())
input6 = int(input())
input7 = int(input())
input8 = int(input())
input9 = int(input())
input10 = int(input())

inputs = [input1, input2, input3, input4, input5, input6, input7, input8, input9, input10]
unique_remains = set([int(i) % 42 for i in inputs])
print(len(unique_remains))
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
10
</pre>
## [1546](https://www.acmicpc.net/problem/1546)



```python
N = int(input())
scores = [int(x) for x in input().split()]
M = max(scores)
new_scores = [s/M * 100 for s in scores]
print(sum(new_scores)/len(new_scores))
```

<pre>
3
40 80 60
75.0
</pre>
## [8958](https://www.acmicpc.net/problem/8958)



```python
def score_of_problem(OX_strings, target_ind):
    if OX_strings[target_ind] == 'O':
        score = 1
        while True:
            try :
                if (target_ind - score >= 0) and OX_strings[target_ind - score] == 'O':
                    score += 1
                else:
                    break
            except:
                break
    else:
        score = 0
    return score

T = int(input())
for t in range(0, T):
    OX_string = input()
    scores = [score_of_problem(OX_string, i) for i in range(0, len(OX_string))]
    print(sum(scores))
```

<pre>
5
OOXXOXXOOO
10
OOXXOOXXOO
9
OXOXOXOXOXOXOX
7
OOOOOOOOOO
55
OOOOXOOOOXOOOOX
30
</pre>
## [4344](https://www.acmicpc.net/problem/4344)



```python
C = int(input())
for c in range(0, C):
    N, *scores = [int(x) for x in input().split()]
    mean = sum(scores) / N
    count = 0
    for s in scores:
        if s > mean:
            count += 1
    ratio = count / N * 100
    print(f'{ratio:.3f}%')
```

<pre>
5
5 50 50 70 80 100
40.000%
7 100 95 90 80 70 60 50
57.143%
3 70 90 80
33.333%
3 70 90 81
66.667%
9 100 99 98 97 96 95 94 93 91
55.556%
</pre>