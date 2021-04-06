---
layout: post
title: VSCode (Visual Studio Code) SSH 원격접속 세팅
subheading: 서버에 원격접속하여 파이썬 코딩하기
author: Jiyoung Min, Kyung Hyun Lee
categories: [Summary & Tips]
tags: [tutorial, server setting, ssh]
banner: https://code.visualstudio.com/assets/blogs/2019/07/25/social-remote-ssh.png
---

## 1. GPU 서버 원격접속

보통 딥러닝을 할 때, 작은 데이터셋과 간단한 아키텍쳐를 가진 네트워크를 사용하여 학습시키는 경우 로컬 노트북이나 데스탑을 통해 학습시킬 수 있으나,      
데이터셋의 크기가 커지고 복잡하고 깊은 네트워크를 학습시키기 위해서는 GPU 서버를 구매하거나 대여하여 사용하게된다.   
**이 포스팅에서는 우리의 로컬 컴퓨터에서 VSCode를 사용하여 서버로 원격접속을 하여 코딩하는 방법에 대해 정리하고자 한다.**


## 2. 로컬 컴퓨터 준비사항

- VSCode가 설치되어 있어야 한다. 공식 홈페이지 (https://code.visualstudio.com/) 에서 본인 로컬 컴퓨터의 OS에 맞춰 다운로드 받은 후 설치하면 된다.

- 이전 [*VSCode (Visual Studio Code) 핵심 단축키*](https://wnet500.github.io/summary%20&%20tips/2021/04/03/VSCode-shortcuts.html) 포스팅에서 언급했듯이, VSCode는 다양한 확장 (extension) 플러그인을 설치하여 원하는 대로 환경을 구성할 수 있는 장점을 가지고 있다. 서버에 원격접속하기 위해 다음 extention을 설치해야 한다.
  - Remote - SSH
  - Remote - SSH: Editing Configuration Files
  
  <img src="https://drive.google.com/uc?export=view&id=1fVDJi795q002JRPW6UOqpdC1xYbZxyab">


## 3. 서버 준비사항

- [여기](https://code.visualstudio.com/docs/remote/linux)에서 VSCode SSH remote를 위해 원격접속 대상인 서버에 설치가 필요한 라이브러리를 확인한다.   
  아래 이미지에서 Base, Remote - SSH Requirements에 빨간색으로 표시된 라이브러리들이 설치 되어야 한다.

  <img src="https://drive.google.com/uc?export=view&id=12HOtU3nSQ08GpKkSDfcqshuuvbJUfF1v">

- 필요한 라이브러리들을 `sudo apt-get install "패키지1" "패키지2" ...`와 같은 커멘드를 사용하여 설치한다.   
  ex. `sudo apt-get install libc6 libstdc++6`

- Anaconda를 사용하는 경우 대부분의 라이브러리를 가지고 있어, libc6과 libstdc++6 정도 추가적으로 설치가 필요하나, 적혀져있는 필요한 모든 라이브러리에 대해 설치 유무를 살펴보고 설치하는 것을 추천한다.


## 4. VSCode SSH config 설정

- 본격적으로 서버에 SSH 원격접속을 하기 위해, 로컬 컴퓨터 VSCode에서 SSH 설정을 해주어야 한다.

- 2번에서 진행한 extention 설치가 잘 되었다면 아래 이미지의 왼쪽에 주황색 박스로 표시된 컴퓨터 모양의 아이콘이 보일 것이다.

- VSCode 왼쪽 하단의 연두색으로 된 >< 표시를 클릭하고, `Remote-SSH: Open Configuration File...`을 클릭한다.
  
    <img src="https://drive.google.com/uc?export=view&id=1AR5dCaGY6RNMcxoK1Ls9qhp2s1ffAr-L">


- `/Users/"username"/.ssh/config`를 선택한 후, config 파일 안에 ssh 정보를 다음과 같이 입력한다.

```
Host "서버 별칭"
    HostName "서버 IP"
    User "서버 유저 아이디"
    Port "서버 접속 포트" 
```

- 예시는 다음과 같다.

```
Host BELab
    HostName 101.101.101.11
    User testuser
    Port 1004
```

## 5. 서버에 SSH 원격 접속

- VSCode 왼쪽 하단의 연두색으로 된 >< 표시를 클릭하고, `Remote-SSH: Connect Current Window to Host...`을 선택한다.   
  만약, 해당 윈도우에서 연결하고 싶지 않다면, 상단에 File > New window를 클릭하여 새로운 윈도우를 만들고 연결한다.

- 4.에서 설정한 "서버 별칭"을 선택한다.

- 상단에 `Enter password for "서버 유저 아이디"@"HostName"`이라는 문구가 보이면, 서버 해당 유저 아이디의 비밀번호를 입력하고 Enter를 눌러준다.

- 왼쪽 하단애 초록색으로 `SSH: "서버 별칭"`이 표시된 것이 보이면 성공한 것이다.


## 6. 파이썬 코드 실행

- 원격접속한 VSCode에서 파이썬을 실행하기 위해 다음과 같은 기본 extension을 설치한다.
  
  - **Python** (파이썬)
  - **Jupyter** (쥬피터 노트북)
  - **Pylance** (Python language support, 코드 작성에 편리)
  - **Python Indent** (파이썬 자동 내어쓰기)
  - **Tabnine Autocomplete AI** or **Visual Studio IntelliCode** or **Kite AutoComplete AI** (코드 추천 및 자동완성)

<br/>

- 파이썬 파일을 저장할 폴더 선택
  Open Folder -> 글쓴이의 경우 홈 디렉토리의 "vscode"라는 폴더 선택 (이미 존재하는 폴더만 선택 가능)

    <img src="https://drive.google.com/uc?export=view&id=1UGgTTmKRbAYdaL5cPOKRSRN3-dGQHfmJ">
<br/>

- 인터프리터 (파이썬 환경) 선택   
  글쓴이의 경우 anaconda 가상환경 중 "torch"라는 가상환경을 선택

    <img src="https://drive.google.com/uc?export=view&id=1Vz-wZttfK9m7LK5hn7z78Pf_MNWPOtO6">  
<br/>

- 파이썬 파일을 생성하고 코드 수행 결과 확인
  
    <img src="https://drive.google.com/uc?export=view&id=13ZkTntzNuNawRazFFk0PuaJUiUOdo0iX">
  