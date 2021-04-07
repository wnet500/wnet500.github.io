---
layout: post
title: VSCode (Visual Studio Code)에 깃허브(Github) 연동
subheading: git으로 버젼관리하며 코딩하기
author: Jiyoung Min, Kyung Hyun Lee
categories: [Summary & Tips]
tags: [tutorial, vscode, git]
banner: https://portswigger.net/cms/images/54/14/6efb9bc5d143-article-190612-github-body-text.jpg
---

## 1. 깃(Git) & 깃허브(GitHub)

- **깃(Git) 이란**?

    > 컴퓨터 파일의 변경사항을 추적하고 여러 명의 사용자들 간에 해당 파일들의 작업을 조율하기 위한 분산 버전 관리 시스템이다.   
    > 소프트웨어 개발에서 소스 코드 관리와 파일의 변경사항을 지속적으로 추적하기 위해 사용될 수 있다.

    > <u> 즉, 깃을 활용하여 버젼 관리를 수월하게 할 수 있다. </u>

- **버젼 관리의 필요성**

    깃의 최고의 장점이 버젼 관리라고 할 수 있다. 왜 코딩할 때 버젼 관리가 필요한지 살펴볼 필요가 있다.

   - 이전 버젼의 코드를 되돌려 살펴볼 수 있으며, 복잡한 코드를 개발할 때 이전 버젼과 코드 추가/수정하여 바뀐 새로운 바젼을 비교해 볼 수 있다. 어디 부분이 어떻게 추가/수정되었는지 확인할 수 있다.

   - 동료들과 함께 개발을 할 때, 파트를 나누고 개발하면서 전체 개발 소스를 서로 공유할 수 있다.

- **깃허브(GitHub) 란?**

    > 분산 버전 관리 툴인 깃(Git)을 사용하는 프로젝트를 지원하는 웹호스팅 서비스이다.   
    
    > <u>깃(Git)이 텍스트 명령어 입력 방식인데 반해, 깃허브는 화려한 그래픽 유저 인터페이스(GUI)를 제공한다.</u>   
    
    > 또한, 각 소스코드 저장소마다 마크다운 기반 위키를 만들 수 있으며, 웹 호스팅도 지원하고 있어 이 블로그와 같이 깃허브 기반의 웹사이트를 개발할 수도 있다.


## 2. VSCode에 연동할 깃허브 저장소 준비

이후 VSCode에 연동할 때 사용할 깃허브 저장소를 준비해 둔다.

- 이미 사용하고 있는 깃허브 저장소가 있고, 그 저장소를 연동할 계획이면 이 스텝을 건너뛰어도 된다.

-  만약, <u>새로 저장소를 만들고 연동할 계획</u>이라면 다음과 같이 진행해 볼 수 있다.   
   (VSCode에서 깃허브를 연동할 당시에 새로운 저장소를 만들 수 있으나, 이 방법을 더 선호한다. VSCode 내 절차가 줄어들고 더 가시적이기 때문이다.)

1. <u>깃허브에 로그인 후, VSCode에 연동할 새 저장소 만들기위해 `New`를 클릭한다.</u>

    <img src="https://drive.google.com/uc?export=view&id=1QR0lBxJBcnUzafNBnRpKsXjq2PraXuU_">

2. <u>저장소에 대한 설정을 완료한 후, 저장소를 생성한다.</u>
   
      - `Repository name`에는 본인이 사용한 저장소 이름을 입력한다. 이 포스팅에서는 test로 설정하였다.
  
      - 해당 저장소를 주로 본인만 사용하고 관리할 수 있도록 `Private` 설정할 지,    
      누구에게나 공개할 수 있도록 `Public` 으로 설정할지 결정한다.

    <img src="https://drive.google.com/uc?export=view&id=1VfWRX99-FLJvy9l655R4hvKRbBV0YHrX">

3. <u>저장소가 생성되면 다음과 같은 화면을 확인할 수 있다.</u>
    
    <img src="https://drive.google.com/uc?export=view&id=1PsEiCuFMLhn9Con_v6PxmwUUq5ITyWox">


## 3. 깃(Git) 설치

- 깃이 설치되어 있는지, 버젼을 확인해 본다.   
  `git --version`

- MacOS
  - 만약, XCode 어플리케이션을 설치했다면 git이 이미 설치되어 있을 것이다. 깃 버젼 확인시 뒤에 (Apple Git) 이라는 문구를 볼 수 있다.    
    하지만, 최신 깃 버젼이랑은 거리가 멀 수 있다. 따라서, 터미널에 다음 커멘드를 실행하여 최신 깃을 설치할 수 있다.
  - `brew install git`

- Window
  - [여기](https://git-scm.com/download)를 클릭하여, 윈도우 깃을 다운받을 수 있다.
<br/>

- Linux (Ubuntu)
  - 이전 [포스팅](https://wnet500.github.io/summary%20&%20tips/2021/04/06/vscode-ssh.html)에서 처럼 우분투 서버에 원격접속하여 VSCode를 사용하는 경우가 이에 해당될 수 있다.
  - `sudo apt-get install git` 명령어를 통해 설치할 수 있다.


## 4. 깃(Git) 초기 설정

- 만약, 처음 깃을 설치한 경우 터미널에서 다음과 같은 설정을 진행해야 한다. 이 정보는 git을 통해 commit을 만들 때 마다 사용될 것이다.   

- 다음 커멘드에서 "John Doe" 대신 본인의 이름 ex. "Jiyoung Min"을,   
johndoe@example.com대신 본인의 이메일 ex. wnet50094@gmail.com을 입력해 준다.    
**깃허브 가입 때 사용한 이메일**을 사용한다.

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

- (optional) 깃허브를 연동할 때, 연동할 로컬 레파지토리 폴더를 만들어 둔다. 글쓴이는 `vscode_projects`라는 폴더를 컴퓨터에 생성해 두었다.


## 5. VSCode에 깃허브 저장소 연동

### 1. 깃허브(GitHub) 로그인 하기

- <u>VSCode 내에서 GitHub에 로그인하기</u>

<img src="https://drive.google.com/uc?export=view&id=1a6XYPc7kqbsaCxdYB_w2URuaKAxUeCT_">

<br/>

- <u>Authorize 페이지에서 Continue 누르고 로그인 완료하기 (이미 로그인이 되어있는 경우 자동 로그인이 됨)</u>

<img src="https://drive.google.com/uc?export=view&id=1ZoauQSbCbaxYR62wCSst-yw2PzR5JHwr">

<br/>


### 2. 깃허브(GitHub) 저장소 클론해 오기

- <u>VSCode에서 `Clone Repository` > `Clone from GitHub` 선택</u>

    <img src="https://drive.google.com/uc?export=view&id=1fis7oP9bVPHa4ii3Nz_hDnm7Qs9d1UHx">

<br/>


- <u>연동할 깃허브 저장소 주소 복사하기</u>   
  (저장소가 Public인 경우 **Clone form GitHub** 아래 탭에 저장소 리스트가 보이고, 선택하면 된다.)

    <img src="https://drive.google.com/uc?export=view&id=1JDdyEkEHdU5mdE_KJv5rH37-Bx7dz4rG">

<br/>


- <u>복사한 깃허브 저장소 주소 붙여넣기</u>

    <img src="https://drive.google.com/uc?export=view&id=1rEGOV9f1cQq4ZN4UgqogvGL4Hn2FE-1g">

<br/>


- <u>깃허브 저장소와 연동될 로컬 저장소 위치 선택하기</u>    
  이 포스팅에서는 `4.` 과정에서 생성한 `vscode_projects`라는 폴더를 선택했다.

    <img src="https://drive.google.com/uc?export=view&id=1pZU1EWTGD2Af_wGc3PfWSZP8OWgkCeC3">

<br/>


- <u>깃허브 저장소 클론이 완료된 것을 확인할 수 있다.</u>

    <img src="https://drive.google.com/uc?export=view&id=1cDEV5UvhQycNOC_fYWGjEgl9BbX5FPSJ">


## 6. VSCode에서 Git commit, push/pull

- <u>아래 인터프리터를 선택해 주고, 테스트 파이썬 파일 만들기</u>  
  조금 더 자세한 내용은 이전 포스팅 VSCode (Visual Studio Code) SSH 원격접속 세팅의 [6. 파이썬 코드 실행](https://wnet500.github.io/summary%20&%20tips/2021/04/06/vscode-ssh.html#h-6-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%BD%94%EB%93%9C-%EC%8B%A4%ED%96%89)을 참고할 수 있다.

    <img src="https://drive.google.com/uc?export=view&id=136zj_DhHBBk9BvhCzb3AjGtCi2D_XXrV">

<br/>


- <u>깃 commit하기</u>   
  py 파일을 클릭하면, 이전과 변경된 사항을 볼 수 있다. 확인하고 커밋하면 된다.

    <img src="https://drive.google.com/uc?export=view&id=1qFSyVz9D2ghxu6PZiF3tgTsbrSFuwL0g">

<br/>


- <u>깃 push하기</u>   
  받아와야 할 변경사항이 있으면 pull도 같이 할 수있다. 이 포스팅에서는 화살표 윗 방향만 있어 push할 변화만 있으므로 push만 하게된다.

    <img src="https://drive.google.com/uc?export=view&id=1EVhgF2LAG8-EIprYuJfYNvzEf1Ycj68C">

<br/>


- <u>깃허브(GitHub) 저장소에서 변화 확인하기</u>

    <img src="https://drive.google.com/uc?export=view&id=175Axc-8VDn9rLA3P1XzPYbMSjvvtBpB2">
