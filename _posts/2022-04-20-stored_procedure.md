---
layout: single
title : "17.스토어드프로시저"
author_profile: true
categories: DB
tag: [DB, SQL, MySQL] 
toc: true
use_math: true

---



**본 내용은 [유튜브 강의](https://www.youtube.com/watch?v=lBk5YhLZevs&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=19)를 스스로 공부하며 중요하다고 생각하는 부분만 정리한 내용입니다.**

<br>

# 스토어드 프로시저

스토어드 프로시저는 MySQL의 내부에서 적절한 프로그래밍 기능을 제공한다.



## 생성

```sql
DELIMITER //
CREATE PROCEDURE 스토어드프로시저이름 (IN 또는 OUT 매개변수)
BEGIN
	SQL 프로그래밍 코드
END //
DELIMITER;
```

https://archemist-hong.github.io/db/SQL%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/



### 입력 매개변수 지정

```sql
IN 입력매개변수이름 데이터형식
```

[동적 SQL](https://archemist-hong.github.io/db/SQL%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/)과 함께 사용이 가능하다.



## 출력 매개변수 지정

```sql
OUT 출력매개변수이름 데이터형식
```

출력매개변수를 지정하고, 프로시저 안에서 SELECT ~ INTO 구문을 활용하여 출력매개변수에 결과를 저장하는 방식으로 리턴이 가능하다.



스토어드 프로시저 안에서 변수를 선언할때는 DECLAR문으로 변수 선언이 필요하다.



## 호출

```sql
CALL 스토어드프로시저이름(전달값); -- 입력 매개변수 지정
```

```sql
CALL 스토어드프로시저이름(@변수명); -- 출력 매개변수 지정
SELECT @변수명;
```

입력매개변수와 출력 매개변수를 동시에 사용하는 것도 가능하다.



## 삭제

```sql
DROP PROCEDURE 스토어드프로시저이름;
```

