---
layout: post
title: 우분투(Ubuntu) 서버에 Anaconda와 Pytorch 세팅
subheading: 딥러닝을 위한 서버 세팅 (2)
author: Jiyoung Min, Kyung Hyun Lee
categories: [Summary & Tips]
tags: [tutorial, server setting]
banner: https://analyticsindiamag.com/wp-content/uploads/2020/11/Pytorch-1600x835.png
---

## 1. 서버에 Ubuntu 20.04 설치

- 부팅 디스크를 만들어서 설치 (Ubuntu 20.04 버젼)


## 2. Ubuntu 유저 생성

### A. <u> 유저 생성하기 </u>

- Ubuntu를 설치하고, root계정으로 CUDA, cuDNN과 같은 GPU연산 세팅이 끝났으면, 새로운 유저 아이디를 만들어 사용하는 것이 좋다.
  다음 커멘드를 통해 유저 아이디 생성하자

- 아래 커멘드에서 "newuser"를 실제 유저가 사용할 아이디로 변경해 주자   
  ex. `sudo adduser wnet500`

- Full Name, Work phone, Other에 이메일 주소를 입력하게 하여 유저를 인식하고 관리하기 편하게 하면 좋다.

```
sudo adduser "newuser"
```

![](https://phoenixnap.com/kb/wp-content/uploads/2019/03/creating-sudo-user-ubuntu1.png)

### B. <u> 유저에게 sudo 권한 부여하기 </u>

- 관리자 유저에게 sudo 권한을 주어 전반적인 관리를 가능하게 할 수 있다. 다음 커멘드를 통해 sudo group에 해당 유저를 추가해 줄 수 있다.

```
sudo usermod -aG sudo "newuser"
```

- `sudo su "newuser"`를 실행하여 새로 생성한 유저 아이디로 로그인할 수 있다.

(2. 내용은 다음 [포스팅](https://phoenixnap.com/kb/how-to-create-sudo-user-on-ubuntu)을 참고했다.)


## 3. Anaconda 설치

- 공식 홈페이지 (https://www.anaconda.com/products/individual)에서 리눅스 x86 버젼을 다운로드
<br/>  
    <img src="https://drive.google.com/uc?export=view&id=1xWbWGBFVMCfI0Ym3CWkNpHsEvJqOdUil">
    
- 터미널에서 bash "다운로드 폴더/다운로드된 파일 이름" 실행   
  ex. `bash ~/Downloads/Anaconda3-2020.11-Linux-x86_64.sh`

- 유저 마다 설치를 해주어야 한다.


## 4. Conda 가상환경 만들기

- 가상환경의 정의와 필요 이유
<br/>

> A virtual environment is a named, isolated, working copy of Python that that maintains its own files, directories, and paths so that you can work with specific versions of libraries or Python itself without affecting other Python projects. Virtual environmets make it easy to cleanly separate different projects and avoid problems with different dependencies and version requiremetns across components. The conda command is the preferred interface for managing intstallations and virtual environments with the Anaconda Python distribution. If you have a vanilla Python installation or other Python distribution see [virtualenv](https://virtualenv.pypa.io/en/latest/)
<br/>

- 다음 커멘드들을 실행하여, 아나콘다 가상환경을 만들 수 있다.   
  -n은 name을 의미한다. "envname"에는 사용할 가상환경 이름을 적어두고, python=x.x에는 파이썬 버젼을 명시하면 된다.
  가장 마지막에 anaconda라고 추가하므로써, 아나콘다에서 기본으로 갖추고있는 파이썬 라이브러리 셋을 가질 수 있다.   
  ex. `conda create -n torch python=3.8 anaconda`
  
```
conda update conda
conda create -n "envname" python=x.x anaconda
```
<br/>

- 다음 커맨드를 통해 제대로 가상환경이 만들어졌는지 가상환경 리스트를 확인할 수 있다.

```
conda info --envs
```
<br/>

- 가상환경이 제대로 만들어진 것을 확인한 후, 생성한 가상환경을 다음과 같이 activate할 수 있다.   
  ex. `conda activate torch`

```
conda activate "envname"
```


## 5. 파이토치(Pytorch) 설치
- 파이토치 홈페이지 (https://pytorch.org/)에서 본인의 CUDA 버젼 및 세팅에 맞게 선택 후, 아래에서 실행할 command 얻기  
<br/>

    <img src="https://drive.google.com/uc?export=view&id=1hHutqTDZzTJTxRsCG_Fksk9gebuh12GX">

- 글쓴이의 경우 가상환경에서 아래 커멘드를 실행하였다.    

```
pip install torch==1.8.1+cu111 torchvision==0.9.1+cu111 torchaudio==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
```

