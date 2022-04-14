---
layout: single
title : "[백준] 2.조건문"
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


# 2.조건문


## [1330](https://www.acmicpc.net/problem/1330)



```python
a, b = [int(x) for x in input().split()] # casting(str -> int)
if a > b :
    print(">")
elif a < b :
    print("<")
else :
    print("==")
```

<pre>
1 2
<
</pre>
## [9498](https://www.acmicpc.net/problem/9498)



```python
score = int(input())
if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
elif score >= 60:
    print("D")
else:
    print("F")
```

<pre>
100
A
</pre>
## [2753](https://www.acmicpc.net/problem/2753)



```python
year = int(input())
is_multiple = lambda x, y: x % y == 0
if is_multiple(year, 400):
    print(1)
elif is_multiple(year, 4) and (not is_multiple(year, 100)) :
    print(1)
else:
    print(0)
```

<pre>
1999
0
</pre>
## [14681](https://www.acmicpc.net/problem/14681)



```python
x = int(input())
y = int(input())

if x > 0:
    if y > 0:
        print(1)
    else:
        print(4)
else:
    if y > 0:
        print(2)
    else:
        print(3)
```

<pre>
12
5
1
</pre>
## [2884](https://www.acmicpc.net/problem/2884)



```python
H, M = [int(t) for t in input().split()] # casting(str -> int)
minutes_sanggeun = H * 60 + M

if (minutes_sanggeun - 45) < 0:
    minutes_changyeong = 24* 60 + (minutes_sanggeun - 45)
else:
    minutes_changyeong = minutes_sanggeun - 45

H_changyeong, M_changyeong = divmod(minutes_changyeong, 60)
print(H_changyeong, M_changyeong)
```

<pre>
0 30
23 45
</pre>
## [2525](https://www.acmicpc.net/problem/2525)



```python
A, B = [int(t) for t in input().split()]
C = int(input())

minutes_now = A * 60 + B
minutes_finished = minutes_now + C

if minutes_finished >= 24 * 60:
    minutes_finished -= 24*60
    
H_finished, M_finished = divmod(minutes_finished, 60)
print(H_finished, M_finished)
```

<pre>
23 48
25
0 13
</pre>
## [2480](https://www.acmicpc.net/problem/2480)



```python
dices = [int(d) for d in input().split()]
dices.sort()

dice1, dice2, dice3 = dices
if (dice1 == dice2) and (dice2 == dice3):
    print(10000 + dice1 * 1000)
elif dice1 == dice2:
    print(1000 + dice1 * 100)
elif dice2 == dice3:
    print(1000 + dice2 * 100)
elif dice1 == dice3:
    print(1000 + dice1 * 100)
else:
    print(max(dices) * 100)
```

<pre>
3 3 6
1300
</pre>