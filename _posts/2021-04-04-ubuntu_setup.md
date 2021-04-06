---
layout: post
title: 우분투(Ubuntu) 서버에 Anaconda & CUDA 설치
subheading: 딥러닝을 위한 서버 세팅
author: Jiyoung Min, Kyung Hyun Lee
categories: [Summary & Tips]
tags: [tutorial, server setting]
banner: https://i1.wp.com/build5nines.com/wp-content/uploads/2019/09/Ubuntu_Featured_Image.jpg?fit=900%2C506&ssl=1
---

## 1. 서버에 Ubuntu 설치
- 부팅 디스크를 만들어서 설치 (Ubuntu 20.04 버젼)


## 2. Chrome 설치
- 파이어 폭스에서 Chrome 설치
- 다운로드 폴더에서 다운된 파일 더블 클릭 


## 3. Anaconda 설치
- 공식 홈페이지 (https://www.anaconda.com/products/individual)에서 리눅스 x86 버젼을 다운로드
    <img src="https://drive.google.com/uc?export=view&id=1xWbWGBFVMCfI0Ym3CWkNpHsEvJqOdUil">
    
- 터미널에서 다운로드폴더로 이동 후, bash "다운로드된 파일 이름"   
  ex. bash ~/Downloads/Anaconda3-2020.11-Linux-x86_64.sh


## 4. CUDA toolkit & cuDNN 설치

- CUDA : NVIDIA GPU 컴퓨팅을 위한 툴킷
- cuDNN : GPU 병렬 처리를 위해 필요

1. <u>CUDA PPA 셋업</u>   
   https://medium.com/@stephengregory_69986 참고
  
> Essentially, we’re adding CUDA to our sources.list, which is the file that’s referenced any time we use the apt package manager to download stuff in the terminal with a command like “sudo apt update”

```
sudo apt update
sudo add-apt-repository ppa:graphics-drivers
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64 /" > /etc/apt/sources.list.d/cuda.list'
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda_learn.list'
```

1. <u> CUDA 패키지 다운로드 (cuDNN 라이브러리 포함) </u>

- CUDA 버젼 선택
  - pytorch를 위해 최신 11.1 버젼 설치 (2021.04.05 기준)   
  
  - tensorflow를 위해 최신 11.0 버젼 설치 (2021.04.05 기준)

  - 2번 째 줄에서 sudo apt install cuda-"버젼", 11.1일 경우 11-1 입력  
  
```
sudo apt update
sudo apt install cuda-11-1
sudo apt install libcudnn7
```

2. <u> CUDA를 PATH에 추가 </u>

- vim 설치가 필요한 경우 설치

```
sudo apt-get install vim
```

- vim을 이용해 .profile 파일 열기

```
sudo vim ~/.profile
```

- vim 사용법
  - sudo vim ~/.profile 이후, `i`를 입력하여 수정모드로 변환
  - 수정 후, `:wq!`를 입력하여 저장 후 종료하기

- 마지막 줄에 다음 라이센스 코드를 추가
  - 아래 코드에서 보이는 코드에서, cuda 버젼에 따라 "cuda-xx.x"을 알맞게 수정하기   
    이 포스팅에서는 cuda 11.1을 사용하므로, "cuda-11.1"을 사용

```
# set PATH for cuda 11.1 installation
if [ -d "/usr/local/cuda-11.1/bin/" ]; then
    export PATH=/usr/local/cuda-11.1/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-11.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
fi
```

3. <u> `nvidia-smi` 터미널 커멘드를 통해 CUDA 및 GPU 정보 확인 </u>
- 본인이 CUDA 11.1을 셋팅했을 지라도, CUDA 11.2와 같이 나타날 수 있다.
  실제로는 11.1으로 사용될 것이므로 크게 걱정하지 않아도 된다.


## 5. 파이토치(Pytorch) 설치
- 파이토치 홈페이지 (https://pytorch.org/)에서 본인의 CUDA 버젼 및 세팅에 맞게 선택 후, 아래 command 얻기   
  <img src="https://drive.google.com/uc?export=view&id=1hHutqTDZzTJTxRsCG_Fksk9gebuh12GX">

- 글쓴이의 경우 아래 커멘드를 실행하였다.    

```
pip install torch==1.8.1+cu111 torchvision==0.9.1+cu111 torchaudio==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
```
 

## 6. Ubuntu에 user만들고 sudo 권한 주기

1. <u> 유저 생성하기 </u>

- Ubuntu를 설치하고, root계정으로 위와 같은 GPU와 딥러닝 프레임워크 사용을 위한 세팅이 끝났으면, 새로운 유저 아이디를 만들어 사용하는 것이 좋다.
  다음 커멘드를 통해 유저 아이디 생성하자.

- 아래 커멘드에서 "newuser"를 실제 유저가 사용할 아이디로 변경해 주자.   
  ex. sudo adduser wnet500

- Full Name, Work phone, Other에 이메일 주소를 입력하게 하여 유저를 인식하고 관리하기 편하게 하면 좋다.

```
sudo adduser "newuser"
```

![](https://phoenixnap.com/kb/wp-content/uploads/2019/03/creating-sudo-user-ubuntu1.png)


2. <u> 유저에게 sudo 권한 부여하기 </u>

- 관리자 유저에게 sudo 권한을 주어 전반적인 관리를 가능하게 할 수 있다. 다음 커멘드를 통해 sudo group에 해당 유저를 추가해 주자.

```
sudo usermod -aG sudo "newuser"
```

## 7. ssh 원격 접속 가능하도록 설정하기

- 