---
layout: single
title : "6.SQL 기본문법"
author_profile: true
categories: DB
tag: [DB, SQL, MySQL] 
toc: true
use_math: true

---



**본 내용은 [유튜브 강의](https://www.youtube.com/watch?v=lBk5YhLZevs&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=7)를 스스로 공부하며 중요하다고 생각하는 부분만 정리한 내용입니다.**

<br>

# SQL 기본 문법



## USE 문

```SQL
USE market_db;
```

> "market_db"라는 데이터베이스를 사용할 것을 선언



USE문을 사용하여 DB를 선택하고, 이후에 테이블을 선택해도 되지만,

market_db.member(market_db 데이터 베이스의 member 테이블) 와 같이 DB를 지정하여 사용할 수 있다.



## SELECT 문

기본 형식: SELECT ~(열이름)  FROM ~(테이블 이름)  WHERE (조건절)



### SQL

``` SQL
SELECT height 키, debut_date "데뷔 일자", addr FROM member WHERE mem_name = "블랙핑크";
```

> member 테이블에서 mem_name이 "블랙핑크"인 데이터의 height, debut_date, addr을 선택
>
> height는 별명 "키", bedut_date는 별명 "데뷔 일자"로 적용하여 보여줌



| 키   | 데뷔 일자  | addr |
| ---- | ---------- | ---- |
| 163  | 2016-08-08 | 경남 |

별명(alias) 지정은 열이름 바로 뒤 콤마 전에 작성하며, 별명에 공백이 포함되는 경우 쌍따옴표로 묶어서 처리한다.

SQL의 문법적 오류는 없어서, 정상적으로 실행되지만 조건에 맞는 데이터가 없어서 결과가 안나올 수 있다.



### 조건절

WHERE 뒤에 오는 조건은 다양하게 적용할 수 있다.

```sql
WHERE height >= 165 AND mem_number > 6;
```

과 같이 여러개의 조건을 AND 또는 OR로 묶어서 처리할 수 있다.



#### BETWEEN

위 문장은 다음 문장과 동일하다.

```SQL
WHERE height BETWEEN 163 AND 165;
```



#### IN

```sql
WHERE addr = '경기' OR addr = '전남' OR addr = '경남';
```

위 문장은 다음 문장과 동일하다.

```sql
WHERE addr IN('경기', '전남', '경남');
```



#### "%", "_"

"%"와 "_"는 모든 글자를 의미하며, LIKE 키워드와 함께 쓰인다.

다만, "%"는 여러 글자를 의미하며, "_"는 한글자를 의미한다.

예를 들어,

"우%"는 "우주소녀" 가 가능하다.

그러나 "우_"는 불가능하며, "\_"를 사용하고 싶은 경우, "우\_\_\_"로 3번 사용해야 한다.



```sql
SELECT * FROM member WHERE mem_name LIKE "우%"
```

위 문장은 다음 문장과 동일하다.

```sql
SELECT * FROM member WHERE mem_name LIKE "우___"
```

