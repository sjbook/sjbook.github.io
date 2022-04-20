---
layout: single
title : "18.스토어드함수와커서"
author_profile: true
categories: DB
tag: [DB, SQL, MySQL] 
toc: true
use_math: true

---



**본 내용은 [유튜브 강의](https://www.youtube.com/watch?v=lBk5YhLZevs&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=20)를 스스로 공부하며 중요하다고 생각하는 부분만 정리한 내용입니다.**

<br>

# 스토어드 함수와 커서



## 스토어드 함수

SUM(), CAST(), CONCAT()과 같은 함수를 사용자가 직접 만들어서 사용할 수 있다.



```sql
DELIMITER //
CREATE FUNCITON 함수이름(매개변수)
	RETURNS 반환형식
BEGIN
	프로그래밍코딩
	RETURN 반환값;
END //
DELIMITER;
```

스토어드 함수의 모든 입력은 입력 매개변수이며, 스토어드 프로시저에서 처럼 IN을 붙이지 않는다.



```sql
CREATE FUNCTION calcYearFunc(dYear INT)
    RETURNS INT
BEGIN
    DECLARE runYear INT; -- 활동기간(연도) 변수 선언
    SET runYear = YEAR(CURDATE()) - dYear; -- 변수에 값 할당
    RETURN runYear;
END $$
DELIMITER ;
```



### 함수 호출

```sql
SELECT 함수이름();
```



```sql
SELECT calcYearFunc(2010) AS '활동햇수';
SELECT calcYearFunc(2013) INTO @debut2013; -- 변수에 할당

SELECT mem_id, mem_name, calcYearFunc(YEAR(debut_date)) AS '활동 햇수' -- SELECT문 함께 사용
    FROM member; 
```



### 함수 삭제

```sql
DROP FUNCTION 함수이름;
```



## 커서

테이블에서 한행씩 작업을 처리하기 위한 방식으로 스토어드 프로시저의 안에 들어간다.



### 커서 작동순서

1. 커서 선언하기
2. 반복조건 선언하기
3. 커서 열기
4. **데이터 가져오기**
5. **데이터 처리하기**
6. 커서 닫기



4번과 5번이 한행마다 반복 수행된다.



### 1. 커서 선언하기

```sql
DECLARE memNumber INT;
DECLARE cnt INT DEFAULT 0;
DECLARE totNumber INT DEFAULT 0;
DECLARE endOfRow BOOLEAN DEFAULT FALSE;
```

변수들을 선언하고 DEFAULT문을 이용하여, 초기값을 0으로 설정



```sql
DECLARE 커서이름 CURSOR FOR
	SELECT 열이름 FROM 테이블이름;
```

커서 선언



```sql
DECLARE memberCursor CURSOR FOR
	SELECT mem_number FROM member;
```



### 2. 반복조건 선언하기

```sql
DECLARE CONTINUE HANDLER
	FOR NOT FOUND SET endOfRow = TRUE;
```

이부분은 거의 바뀌지 않고 그대로 사용된다.



### 3. 커서 열기

```sql
OPEN 커서이름;
```



```sql
OPEN memberCursor;
```



### 4. 행 반복하기

```sql
cursor_loop: LOOP
	이 부분을 반복
END LOOP cursor_loop;
```



```sql
cursor_loop: LOOP
	FETCH memberCursor INTO memNumber; -- memNumber 변수에 memberCursor의 값을 가져옴
	
	IF endOfRow THEN -- endOfRow 변수가 TRUE가 되면, cursor loop를 빠져나감
		LEAVE cursor_loop;
	END IF;
	
	SET cnt = cnt + 1; -- 함수의 작업 내용
	SET totNumber = totNumber + memNumber;
	
END LOOP cursor_loop;
```



루프를 빠져나오면, 평균 인원수를 계산한다.

```sql
SELECT (totNumber/cnt) AS '회원의 평균 인원 수';
```



### 5. 커서 닫기

```sql
CLOSE 커서이름;
```



```sql
CLOSE memberCursor;
```



1 ~ 5까지의 모든 과정은 스토어드 프로시저를 생성하고, 프로시저의 안쪽 내용에 들어간다.

생성된 스토어드 프로시저를 호출함으로써 실행할 수 있다.
