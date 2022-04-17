---
layout: single
title : "3.DB 모델링"
author_profile: true
categories: DB
tag: [DB, SQL, MySQL] 
toc: true
use_math: true

---



**본 내용은 [유튜브 강의](https://www.youtube.com/watch?v=j2DAiY-OXGs&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=4)를 스스로 공부하며 중요하다고 생각하는 부분만 정리한 내용입니다.**

<br>

# DB 모델링



이름, 주민등록번호, 주소와 같은 정보들은 "직원 테이블"로 만들 수 있다.

비슷하게 제품이름, 가격, 제조일자, ... 와 같은 정보들은 "제품 테이블"로 만들 수 있다.



## 테이블



직원 테이블

| 아이디       | 회원이름 | 주소        |
| ------------ | -------- | ----------- |
| hjy_stat     | 홍주영   | 광주 남구   |
| yb7410       | 진영봉   | 서울 관악구 |
| jeoseungseok | 이승석   | 서울 은평구 |



열이름 : 아이디, 회원이름, 주소

행: row

열 : column

**Primary key(기본키)**: 각행을 구분하는 유일한 값으로, 열에 지정함(ex 아이디, 회원이름, 주소 중 사용자가 선택)

기본키의 조건

- 중복이 되면 안된다.
- 값이 없으면(Null)안되며 반드시 모든 행에 대해 값을 가져야 한다.

데이터 형식 : 문자, 날짜, 정수,... 등