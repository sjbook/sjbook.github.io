---
layout: single
title : "2.MySQL설치"
author_profile: true
categories: DB
tag: [DB, SQL, MySQL] 
toc: true
use_math: true
---



**본 내용은 [유튜브 강의](https://www.youtube.com/watch?v=8r1W_7nuo2U&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=3)를 스스로 공부하며 중요하다고 생각하는 부분만 정리한 내용입니다.**

<br>

# MySQL 8.0 설치



- 무료 : Community Edition
- 상용 : Standard, Enterprise 등



강의 영상의 카페 링크에서 제공하는 "mysql-installer-community-8.0.21.0.msi" 파일을 활용하여 설치하였습니다.



## 설치 옵션

Custom을 선택 후 모두 default로 다음으로 진행하였습니다.

포트 번호는 3306번으로 기억합니다.

### Products

![캡처](../../images/2022-04-16-install_MySQL/MySQL_install.PNG)

강의와 같이 3개의 Product만을 설치하였습니다.



### Authentication method

Authentication method는 추후 python연결을 위해, 강의와 같이 "Use Legacy Authentication Method"를 선택하였습니다.



모두 초록색으로 설치가 잘 완료되면 끝입니다.



## Test

설치가 모두 끝난 이후에는 MySQL Workbench 8.0 CE로 실행합니다.

Local instance로 설치시 설정했던 root 계정의 비밀번호를 입력하고 접속합니다.

![MySQL_test](../../images/2022-04-16-install_MySQL/MySQL_test.PNG)

SHOW DATABASES 명령어를 입력후 번개모양(실행버튼)을 클릭해서, 다음과 같은 창이 뜨면 성공입니다.