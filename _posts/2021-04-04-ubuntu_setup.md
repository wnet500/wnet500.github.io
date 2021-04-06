---
layout: post
title: 우분투(Ubuntu) 서버에 Anaconda, CUDA, Pytorch 세팅
subheading: 딥러닝을 위한 서버 세팅
author: Jiyoung Min, Kyung Hyun Lee
categories: [Summary & Tips]
tags: [tutorial, server setting]
banner: https://i.pinimg.com/564x/8d/dd/29/8ddd294fc0582e519a81670baa8fd1c1.jpg
---

## 1. 서버에 Ubuntu 20.04 설치
- 부팅 디스크를 만들어서 설치 (Ubuntu 20.04 버젼)


## 2. Anaconda 설치
- 공식 홈페이지 (https://www.anaconda.com/products/individual)에서 리눅스 x86 버젼을 다운로드
<br/>  
    <img src="https://drive.google.com/uc?export=view&id=1xWbWGBFVMCfI0Ym3CWkNpHsEvJqOdUil">
    
- 터미널에서 다운로드 폴더로 이동 후, bash "다운로드된 파일 이름"   
  ex. `bash ~/Downloads/Anaconda3-2020.11-Linux-x86_64.sh`


## 3. CUDA toolkit & cuDNN 설치

- CUDA : NVIDIA GPU 컴퓨팅을 위한 툴킷
- cuDNN : GPU 병렬 처리를 위해 필요

### A. <u>CUDA PPA 셋업</u>   

> CUDA PPA란?  
> Essentially, we’re adding CUDA to our sources.list, which is the file that’s referenced any time we use the apt package manager to download stuff in the terminal with a command like “sudo apt update”

- 다음 커멘드들을 실행하기

```
sudo apt update
sudo add-apt-repository ppa:graphics-drivers
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64 /" > /etc/apt/sources.list.d/cuda.list'
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda_learn.list'
```

### B. <u> CUDA 패키지 다운로드 (cuDNN 라이브러리 포함) </u>

- CUDA 버젼 선택
  - pytorch를 위해 최신 11.1 버젼 설치 (2021.04.05 기준)   
  - 2번 째 줄에서 sudo apt install cuda-"버젼", 11.1일 경우 11-1 입력  
  
```
sudo apt update
sudo apt install cuda-11-1
sudo apt install libcudnn7
```

### C. <u> CUDA를 PATH에 추가 </u>

- vim 설치가 필요한 경우 설치

```
sudo apt-get install vim
```
<br/>

- vim을 이용해 .profile 파일 열기

```
sudo vim ~/.profile
```
<br/>

- vim 사용법
  - sudo vim ~/.profile 이후, `i`를 입력하여 수정모드로 변환
  - 수정 후, `:wq!`를 입력하여 저장 후 종료하기
<br/>

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

### D. <u> CUDA 및 GPU 정보 확인 </u>

- `nvidia-smi` 커멘드 실행하기

- 본인이 CUDA 11.1을 셋팅했을 지라도, CUDA 11.2와 같이 나타날 수 있다.
  실제로는 11.1으로 사용될 것이므로 크게 걱정하지 않아도 된다.

(3. 내용은 다음 [포스팅](https://medium.com/@stephengregory_69986/installing-cuda-10-1-on-ubuntu-20-04-e562a5e724a0)을 참고했다.)


## 4. 파이토치(Pytorch) 설치
- 파이토치 홈페이지 (https://pytorch.org/)에서 본인의 CUDA 버젼 및 세팅에 맞게 선택 후, 아래 command 얻기  
<br/>

    <img src="https://drive.google.com/uc?export=view&id=1hHutqTDZzTJTxRsCG_Fksk9gebuh12GX">

- 글쓴이의 경우 아래 커멘드를 실행하였다.    

```
pip install torch==1.8.1+cu111 torchvision==0.9.1+cu111 torchaudio==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
```
 