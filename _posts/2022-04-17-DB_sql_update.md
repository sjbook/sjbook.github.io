---
layout: single
title : "8.데이터 변경을 위한 SQL문"
author_profile: true
categories: DB
tag: [DB, SQL, MySQL] 
toc: true
use_math: true
---



**본 내용은 [유튜브 강의](https://www.youtube.com/watch?v=lBk5YhLZevs&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=9)를 스스로 공부하며 중요하다고 생각하는 부분만 정리한 내용입니다.**

<br>

# 데이터 변경을 위한 SQL문



## INSERT



```sql
INSERT INTO 테이블이름 (열1, 열2, ...) VALUES (값1, 값2, ...);
```

열 이름을 생략할 수 있으나, 열 이름을 정확히 지정하는 것을 권장

열의 순서는 테이블에 있는 열 순서와 반드시 같을 필요 없으나, 열과 값이 서로 순서대로 대응되면 된다.



```sql
USE market_db;
CREATE TABLE hongong1 (toy_id  INT, toy_name CHAR(4), age INT);
INSERT INTO hongong1 VALUES (1, '우디', 25);
```

> 혼공1 테이블 생성후, 값 입력(순서대로 toy_id, toy_name, age)



```sql
INSERT INTO hongong1 (toy_name, age, toy_id) VALUES ('홍주영', 27, 2);
```

> 열이름을 명시하면, 순서에 관계없이 값을 입력할 수 있다.



```sql
INSERT INTO hongong1(toy_id, toy_name) VALUES (2, '버즈');
```

> 열이름을 명시하면, 원하는 열에만 값을 입력할 수 있다.



## Auto_Increment

의미는 따로 없지만, 자동생성하여 구별이 필요한 경우에 사용한다.

NULL로 입력하면, 자동으로 생성되며, 반드시 기본키로 지정해야 한다.



```sql
CREATE TABLE hongong2 ( 
   toy_id  INT AUTO_INCREMENT PRIMARY KEY, 
   toy_name CHAR(4), 
   age INT);
```

> toy_id는 auto increment로 생성되며, 기본키이다.



```sql
INSERT INTO hongong2 VALUES (NULL, '보핍', 25);
```

> 데이터 입력시 NULL 값을 입력하면, toy_id는 자동으로 생성되어 1값이 부여된다.



auto increment로 어디까지 입력되었는지 확인하고 싶은 경우,

```sql
SELECT LAST_INSERT_ID();
```

로 확인할 수 있다.



auto increment의 시작 숫자를 변경하고 싶은 경우 다음과 같이 지정한다.

```sql
ALTER TABLE hongong2 AUTO_INCREMENT=100;
```

이후 생성되는 toy_id는 100부터 생성된다. (100, 101, 102, ...)



```sql
SET @@auto_increment_increment=3;
```

위 명령을 지정하면, auto increment의 자동증가되는 값을 변경한다. (1 => 3)

(100, 103, 106, 109, ...)



## DESC

테이블의 구조 및 데이터 타입등을 확인할 수 있다.



```sql
DESC hongong2;
```

> hongong2 테이블의 구조 확인



## INSERT INTO ~ SELECT

많은 양의 데이터를 한번에 입력하는 경우 Insert into ~ select 구문을 활용한다.



```sql
CREATE TABLE city_popul ( city_name CHAR(35), population INT);
INSERT INTO city_popul
    SELECT Name, Population FROM world.city;
```

> city_popul 테이블을 만들고, world DB의 city table에서 name과 population을 가져와 한꺼번에 입력



## UPDATE

Work bench의 Edit => Preference => SQL Editor => safe update 체크 해제 후 재접속



```sql
UPDATE 테이블이름
	SET 열1 = 값1, 열2 = 값2, ...
	WHERE 조건;
```



조건없이 사용하면, 테이블의 모든 값이 변경되므로 대부분 WHERE 절과 함께 사용된다.

```sql
UPDATE city_popul
    SET city_name = '뉴욕', population = 0
    WHERE city_name = 'New York';
```

> city_popul 테이블에서 city_name이 "New York"인곳의 name을 "뉴욕"으로, population은 0으로 변경



그러나 아주 가끔 WHERE문 없이 사용되는 경우가 있다.

EX) 인구의 단위를 만명 단위로 바꾸고 싶은 경우

```sql
UPDATE city_popul
    SET population = population / 10000 ;
```

> city_popul 테이블에서 population을 population / 10000으로 변경



## DELETE



```sql
DELETE FROM 테이블이름 WHERE 조건
```



```sql
DELETE FROM city_popul 
    WHERE city_name LIKE 'New%'
    LIMIT 5;
```

> city_popul 테이블에서 city_name이 New로 시작하는 도시들을 5개까지 삭제