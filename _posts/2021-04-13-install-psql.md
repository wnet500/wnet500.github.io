---
layout: post
title: 우분투(Ubuntu) 서버에 PostgreSQL 설치
subheading: DB 조작 및 관리
author: Jiyoung Min
categories: [데이터베이스]
tags: [tutorial, psql]
banner: https://i2.wp.com/itsfoss.com/wp-content/uploads/2019/08/install-postgresql-ubuntu.png?fit=800%2C450&ssl=1
---

## 1. PostgreSQL 개요

### A. 소개

위키피디아에 의하면 PostgreSQL은 다음과 같다.
> PostgreSQL, also known as Postgres, is a free and open-source relational database management system emphasizing extensibility and SQL compliance.

즉, <u>무료의 오픈소스 기반 관계형 데이터베이스 관리 시스템</u>이며,   
최근들어 각광을 받고 있는 시스템이라고 할 수 있다.

### B. 특징

- 가장 진보한 오픈소스 데이터베이스 시스템이라고 볼 수 있다.
- Linux, MacOS, Windows 등의 OS를 지원하고 있다.
- 완전 무료의 소프트웨어이다.
- 확장성이 매우 좋다는 큰 장점을 가지고 있다.
- 오픈소스 커뮤니티가 있으며, 많은 기업들이 기술지원 서비스를 하고 있다.
- DB 엔진 랭킹 4위이며, 점점 더 사용량이 많아지고 있는 추세이다.

  <img src="https://drive.google.com/uc?export=view&id=1YeFp8hhJ8UtzA0Pk8J3b2XgpJ3y0lHJa">

## 2. Ubuntu 20.04 서버에 PostgreSQL 설치

- 다음 커멘드로, Postgres 패키지와 추가적인 유틸리티를 가지고 있는 -contrib 패키지를 설치한다.

```
sudo apt install postgresql postgresql-contrib
```

- 설치가 완료되었으면, `postgres`라는 user가 우분투 서버에 생성되었다.   
  다음 커맨드를 통해 `postgres` 계정으로 로그인할 수 있다. 다시 본인의 계정으로 돌아오기 위해서는 `exit` 커맨드를 치면되다.

```
sudo -i -u postgres
```

- `psql`이라는 커맨드를 치면, PostgreSQL prompt를 실행할 수 있다. `postgres=#`가 보이는 것을 확인할 수 있다.   
  prompt를 종료하기 위해서는 `\q` 커맨드를 실행하면 된다.

```
pqsl
postgres=#
```

- 다음 커맨드를 통해, <u>한 번에 postgres 계정을 통해 PostgreSQL prompt를 실행할 수 있다.</u>

```
sudo -u postgres psql
```

## 3. 새로운 Role과 DB 생성하기
쉽게 말해, postgres의 계정을 생성하고, 생성된 계정이 누릴 수 있는 권한을 부여하고 제한하는 과정이다.

### A. 계정 생성
- 설치한 바로 이후에는, 가장 큰 권한을 가지고 있는 postgres 계정을 통해 계정을 생성할 수 있다.
일단, 먼저 데이터베이스 생성, 새로운 롤 생성 등을 포함한 큰 권한을 가지고 있는 `superuser`를 생성할 수 있다.    
**PostgreSQL의 계정을 Ubuntu 계정과 동일하게 생성하는 것을 추천한다.**

```
sudo -u postgres createuser --interactive
```
[Output]
```
Enter name of role to add: NEW_USER_ID
Shall the new role be a superuser? (y/n) y

<예시>
Enter name of role to add: wnet50094
Shall the new role be a superuser? (y/n) y
```

### B. DB 생성
- 다음 커멘드를 통해 DB를 생성할 수 있다. 지금 이 단계에서 DB를 생성할 수 있는 계정은 `postgres`와 이전 단계에서 생성한 `userid` 이다.   

- dbname을 위 생성한 userid와 동일하게 할 것을 추천한다.   
**postgres userid와 같은 이름으로 db를 생성하게 되면, 자동으로 그 userid에 db가 connection되기 때문이다.**

```
sudo -u postgres createdb DBNAME

<예시>
sudo -u postgres createdb wnet50094
```

- <u>간단히 정리해 보자면, `Ubuntu 계정` = `PostgreSQL 계정` = `DB 이름` 으로 하면 편하다.</u>
</br>

- dbname을 userid가 아닌 다른 이름으로 만들고 싶을 경우,   
슈퍼 유저일 경우에 `sudo -u SUPER_USER_ID createdb DESIRED_DBNAME` 커맨드를 수행하면 된다.

### C. 새로운 계정으로 psql 실행

우분투와 포스트그리 두 계정이 같다면, 본인의 ubuntu 계정에 로그인 한 후, `psql` 커맨드를 치기만 하면 된다.

다른 경우 `sudo -u NEW_USER_ID psql postgres` 커맨드를 치면된다. NEW_USER_ID에 새로 생성한 계정의 이름을 넣으면 된다.

## 4. DBeaver에서 생성한 DB에 connection 세팅하기

### A. DBeaver
> DBeaver는 클라이언트 소프트웨어 어플리케이션이자 데이터베이스 관리 도구이다.     
> DBeaver에서 PostgreSQL뿐 만 아니라 Oracle 등 다양한 관계형 데이터베이스에 connection을 만들어 접속하여 DB를 관리하고 쿼리를 수행할 수 있다.


- PostgreSQL만 사용하는 경우 Pgadmin을 사용해 볼 수 있다.    
하지만 글쓴이는 DBeaver가 가지는 여러 유용한 기능들 ex. 마우스 클릭으로 csv 저장, 강력한 자동 추천 완성 등을 사용하기 위해 DBeaver를 쓰는 것을 추천한다.

### B. connection 만들기

- General (또는 본인이 생성한 프로젝트) > Connections에서 마우스 우측클릭 후, `Create > Connection` 선택, PostgreSQL 클릭

- 본인의 local 컴퓨터에 있는 DB를 연결할 경우, 다음을 실행하고 왼쪽 아래 `Test Connection ...`을 클릭하여 잘 연결되는 것이 확인되면 완료를 누른다.    
  PostgreSQL의 포트는 기본으로 5432로 세팅되어 있다.
  <img src="https://drive.google.com/uc?export=view&id=1du7gVf2t7L-74q3wTNNAoEsp5o5Thc3H">

- 만약, Ubuntu 서버에 설치된 PostgreSQL에 연결하는 경우 추가로 SSH 탭에서 다음과 같은 정보를 입력하고 `Test Connection ...`을 클릭하여 잘 연결되는 것이 확인되면 완료를 누른다.
    <img src="https://drive.google.com/uc?export=view&id=1jjomqA4qMFchDMj9-zefAadjG8VWOpsy">