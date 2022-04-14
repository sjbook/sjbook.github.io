---
layout: single
title : "[백준] 6.문자열"
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


# 문자열


## [11654](https://www.acmicpc.net/step/7)



```python
_input = input()
print(ord(_input))
```

<pre>
A
65
</pre>
- ord(문자) : 문자의 아스키 코드값을 리턴

- chr(숫자) : 숫자에 해당하는 아스키 문자를 리턴


## [11720](https://www.acmicpc.net/problem/11720)



```python
N = int(input())
sequence = input()
print(sum([int(number) for number in sequence]))
```

<pre>
11
10987654321
46
</pre>
## [10809](https://www.acmicpc.net/problem/10809)



```python
S = input()
alphabets = 'abcdefghijklmnopqrstuvwxyz'
alphabet_indexes = []
for alphabet_index in range(0, len(alphabets)):
    alphabet = alphabets[alphabet_index]
    for index in range(0, len(S)):
        if S[index] == alphabet:
            alphabet_indexes.append(index)
            break
        else:
            if index == (len(S)-1):
                alphabet_indexes.append(-1)
                
for i in range(0, len(alphabet_indexes)):
    print(alphabet_indexes[i], end = ' ')
```

<pre>
baekjoon
1 0 -1 -1 2 -1 -1 -1 -1 4 3 -1 -1 7 5 -1 -1 -1 -1 -1 -1 -1 -1 -1 -1 -1 
</pre>
## [2675](https://www.acmicpc.net/problem/2675)



```python
T = int(input())
for i in range(0, T):
    R, S = input().split()
    R = int(R)
    P_list = [char * R for char in S]
    P = ''.join(P_list)
    print(P)
```

<pre>
2
3 ABC
AAABBBCCC
5 /HTP
/////HHHHHTTTTTPPPPP
</pre>
## [1157](https://www.acmicpc.net/problem/1157)



```python
word = input().upper()
alphabet_counts = []
alphabets = 'abcdefghijklmnopqrstuvwxyz'
alphabets = alphabets.upper()
for i in range(0, len(alphabets)):
    count = 0
    for char in word:
        if alphabets[i] == char:
            count += 1
    alphabet_counts.append(count)

index = []
count_max = max(alphabet_counts)
for i in range(0, len(alphabet_counts)):
    if count_max == alphabet_counts[i]:
        index.append(i)
        
if len(index) >= 2 :
    print("?")
else:
    print(alphabets[index[0]])
```

<pre>
baaa
A
</pre>
## [1152](https://www.acmicpc.net/problem/1152)



```python
words = input().split()
print(len(words))
```

<pre>
The Curious Case of Benjamin Button
6
</pre>
## [2908](https://www.acmicpc.net/problem/2908)



```python
A, B = input().split()
A = int(A[::-1])
B = int(B[::-1])
print(max([A, B]))
```

<pre>
221 231
132
</pre>
## [5622](https://www.acmicpc.net/problem/5622)



```python
words = input()

character_groups = ['', 'ABC', 'DEF', 'GHI', 'JKL', 'MNO', 'PQRS', 'TUV', 'WXYZ', 'OPERATOR']
number_groups = list(range(1, 10)) + [0]

def translate_character(character : str, character_groups : list[str], number_groups : list[int]) -> int:
    for i in range(0, len(character_groups)):
        if character in character_groups[i]:
            return number_groups[i]
            break

time = 0
for char in words:
    time += translate_character(char, character_groups, number_groups) + 1

print(time)
```

<pre>
UNUCIC
36
</pre>
## [2941](https://www.acmicpc.net/problem/2941)



```python
_input = input()
two_char_croatia_alphabet = ['c=', 'c-', 'd-', 'lj', 'nj', 's=', 'z=']
count = 0
i = 0
while i < len(_input):
    if _input[i:(i+3)] == 'dz=':
        count += 1
        i += 3
    elif _input[i:(i+2)] in two_char_croatia_alphabet:
        count += 1
        i += 2
    else:
        count += 1
        i += 1
print(count)
```

<pre>
dz=ak
3
</pre>
# [1316](https://www.acmicpc.net/problem/1316)



```python
N = int(input())

def is_group_word(word: str) -> bool:
    for index in range(0, len(word)-1):
        char = word[index]
        if (word[index] != word[index + 1]) and (word[index] in word[index + 1:]):
            return False
    return True            
        
count = 0
for n in range(0, N):
    word = input()
    if is_group_word(word):
        count += 1
print(count)
```

<pre>
1
z
1
</pre>
- 그룹단어 아이디어:



'aabca'와 같은 단어에서 a라고 하는 단어가 연속해서 나오다가 b라는 단어로 바뀌었는데, b뒤의 문자열 'ca'에서 'a'가 있으면 그룹단어가 아님

