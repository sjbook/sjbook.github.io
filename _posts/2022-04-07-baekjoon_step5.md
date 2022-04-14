---
layout: single
title : "[백준] 5.함수"
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


# 함수


## [15596](https://www.acmicpc.net/problem/15596)



```python
def solve(a: list[int]) -> int:
    return sum(a)
```

## [4673](https://www.acmicpc.net/problem/4673)



```python
def d(num: int) -> int:
    num_str :str = str(num)
    return num + sum([int(n) for n in num_str])

natural_numbers = set(range(1, 10001))
generated_numbers = set()
for number in natural_numbers:`b
    generated_number = d(number)
    generated_numbers.add(generated_number)

self_numbers = sorted(natural_numbers - generated_numbers)
for self_number in self_numbers:
    print(self_number)
```

시간 초과 주의!



중복을 제거할때는 set 자료형을 잘 사용하자!


## [1065](https://www.acmicpc.net/problem/1065)



```python
def is_hansu(X: int) -> bool:
    X = str(X)
    if len(X) == 1:
        return True
    digit_diffs = set(int(X[i]) - int(X[i-1]) for i in range(1, len(X)))
    if len(digit_diffs) == 1:
        return True
    else:
        return False

N = int(input())
hansus = []
for n in range(1, N + 1):
    if is_hansu(n):
        hansus.append(n)
print(len(hansus))
```

<pre>
500
119
</pre>