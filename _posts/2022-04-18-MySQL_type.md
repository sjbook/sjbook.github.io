---
layout: single
title : "9.MySQL 데이터형식"
author_profile: true
categories: DB
tag: [DB, SQL, MySQL] 
toc: true
use_math: true

---



**본 내용은 [유튜브 강의](https://www.youtube.com/watch?v=lBk5YhLZevs&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=10)를 스스로 공부하며 중요하다고 생각하는 부분만 정리한 내용입니다.**

<br>

# MySQL의 데이터 형식



## 정수

| 타입     | 바이트 | 범위              |
| -------- | ------ | ----------------- |
| TINYINT  | 1      | -128 ~ 127        |
| SMALLINT | 2      | -32768 ~ 32767    |
| INT      | 4      | 약 - 21억 ~ 21억  |
| BIGINT   | 8      | 약 -900경 ~ 900경 |



입력값의 범위를 넘어가는 경우 Out of range Error 발생 가능



### UNSIGNED

각 타입을 부호가 없는 양의 정수로 사용할 수 있다.

```sql
TINYINT UNSIGNED
```

-128 ~ 127 => 0 ~ 255



## 문자

| 타입    | 범위      | 사용처                  | 비고        |
| ------- | --------- | ----------------------- | ----------- |
| CHAR    | 255자까지 | 글자 수가 고정적인 경우 | 속도가 빠름 |
| VARCHAR | 16383까지 | 글자 수가 가변적인 경우 | 공간 효율적 |



숫자로서 의미가 없는 숫자로 이루어진경우에는 문자로 취급

- 크다/ 작다 : 대소개념이 없는경우
- 더하기 / 빼기 연산의 의미가 없는 경우

EX) 전화번호 : 숫자로 이루어져 있지만 숫자로서 의미가 없으므로 문자취급



## 대량의 데이터 형식

LONGTEXT : 자막과 같이 매우 긴 문자

LONGBLOB: 동영상과 같은 용량이 큰 이진데이터



## 실수

| 타입   | 바이트 | 범위                  |
| ------ | ------ | --------------------- |
| FLOAT  | 4      | 소수점아래 7자리까지  |
| DOUBLE | 8      | 소수점아래 15자리까지 |



## 날짜

| 타입     | 바이트 | 형식                | 비고              |
| -------- | ------ | ------------------- | ----------------- |
| DATE     | 3      | YYYY-MM-DD          | 날짜만 저장       |
| TIME     | 3      | HH:MM:SS            | 시간만 저장       |
| DATETIME | 8      | YYYY-MM-DD HH:MM:SS | 날짜 및 시간 저장 |



## 변수

변수는 영구저장되지 않으며, 임시로 저장되어 workbench 종료시 또는 다른 계정 접근시 활용할 수 없다.



### 변수의 선언 및 대입

```sql
SET @변수이름 = 변수의값;
```



### 변수 값 출력

```sql
SELECT @변수이름;
```



### 변수를 활용한 SQL

```sql
SET @txt = '연습';
SET @height = 165;
SELECT @txt, mem_name FROM member WHERE height > @height;
```



## PREPARE ~ EXECUTE

그러나 'LIMIT @count' 형태로는 사용할 수 없다.

이런 경우 PREPARE ~ EXECUTE문을 사용한다.



```sql
SET @count = 3;
PREPARE mySQL FROM 'SELECT mem_name, height FROM member ORDER BY height LIMIT ?';
EXECUTE mySQL USING @count;
```

PREPARE문으로 ?가 포함된 쿼리를 mySQL에 저장하고, EXECUTE문으로 mySQL의 ?를 @count 변수를 이용하여 대체해서 실행한다.



## 데이터 형 변환



### 명시적 형 변환



```sql
CAST(값 AS 데이터형식(길이))
CONVER(값, 데이터형식(길이))
```



**SIGNED**: 부호가 있는 정수형 타입 (실수 => 정수로 캐스팅 하는 경우 사용)

```sql
SELECT CAST(AVG(height) AS SIGNED) FROM member;
```



명시적 형 변환은 문자를 날짜로 바꾸는 경우에도 종종 사용된다.

```sql
SELECT CAST('2021/04/18' AS DATE);
SELECT CONVERT('2021/04/18', DATE);
```



### 암시적 형 변환

명시적으로 변환을 지정하지 않아도 알아서 타입이 변환되어 연산된다.



```sql
SELECT '100' + '200';
```

위 SQL을 실행하면 문자가 정수로 변환되어, 300이 출력된다.



문자열을 이어붙이고 싶은겨우 CONCAT()을 사용한다.

```sql
SELECT CONCAT('100' ,'200');
```



```sql
SELECT CONCAT(100 ,'200');
```

위와 같이 한쪽이 정수인경우에도 문자형으로 자동 형변환되어, '100200'이 출력된다.
