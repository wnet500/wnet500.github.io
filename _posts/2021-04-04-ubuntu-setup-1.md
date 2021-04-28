---
layout: post
title: 우분투(Ubuntu) 서버에 CUDA와 cuDNN 설치
subheading: 딥러닝을 위한 서버 세팅 (1)
author: Jiyoung Min, Kyung Hyun Lee
categories: [리눅스 서버, 인공지능 & 딥러닝]
tags: [tips, server setting]
banner: https://res.cloudinary.com/practicaldev/image/fetch/s--5Epkp0zJ--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://www.tipard.com/images/video/cuda.jpg
---

## 1. 서버에 Ubuntu 20.04 설치

- 부팅 디스크를 만들어서 설치 (Ubuntu 20.04 버젼)


## 2. CUDA toolkit & cuDNN 설치

- CUDA : NVIDIA GPU 컴퓨팅을 위한 툴킷
- cuDNN : GPU 병렬 처리를 위해 필요

### A. <u>NVIDIA driver 설치</u>

- 다음 커맨드 실행하기

```
sudo apt install nvidia-driver-460
```

### B. <u>CUDA PPA 셋업</u>   

> CUDA PPA란?  
> Essentially, we’re adding CUDA to our sources.list, which is the file that’s referenced any time we use the apt package manager to download stuff in the terminal with a command like “sudo apt update”

- 다음 커멘드들 실행하기

- 만약, 우분투의 버전이 18.04인 경우, 아래 코드에서 모든 `ubuntu2004`를 `ubuntu1804`로 수정해 준다.

```
sudo apt update
sudo add-apt-repository ppa:graphics-drivers
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64 /" > /etc/apt/sources.list.d/cuda.list'
sudo bash -c 'echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu2004/x86_64 /" > /etc/apt/sources.list.d/cuda_learn.list'
```

### C. <u> CUDA 패키지 다운로드 (cuDNN 라이브러리 포함) </u>

- CUDA 버젼 선택
  - pytorch를 위해 11.1 버젼 설치 결정 (2021.04.05 기준)   
    [여기](https://pytorch.org/get-started/locally/)에서 사용가능한 CUDA 버젼 확인 및 버젼 결정

  - 2번 째 줄에서 sudo apt install cuda-"버젼", 11.1일 경우 버젼에 11-1 입력  
  - 3번 째 줄에서 sudo apt install libcudnn"Major 버젼", CUDA 11.1의 경우 cuDNN 8.x.x버젼이 필요하므로, Major 버젼에 8 입력    
    (CUDA와 cuDNN의 compatibility는 [여기](https://docs.nvidia.com/deeplearning/cudnn/support-matrix/index.html)에서 확인해 볼 수 있다.)
  
```
sudo apt update
sudo apt install cuda-11-1
sudo apt install libcudnn8
```

### D. <u> CUDA를 PATH에 추가 </u>

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
  - 수정 후, esc를 누르고 `:wq!`를 입력하여 저장 후 종료하기

<br/>

- 마지막 줄에 다음 라이센스 코드를 추가
  - 아래 코드에서 보이는 코드에서, cuda 버젼에 따라 모든 "cuda-xx.x"을 알맞게 수정하기   
    이 포스팅에서는 cuda 11.1을 사용하므로, "cuda-11.1"을 사용

```
# set PATH for cuda 11.1 installation
if [ -d "/usr/local/cuda-11.1/bin/" ]; then
    export PATH=/usr/local/cuda-11.1/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-11.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
fi
```

### E. <u> CUDA 및 GPU 정보 확인 </u>

- `nvidia-smi` 커멘드 실행하기

- 본인이 CUDA 11.1을 셋팅했을 지라도, CUDA 11.2와 같이 나타날 수 있다.
  실제로는 11.1으로 사용될 것이므로 크게 걱정하지 않아도 된다.
<br/>

  <img src="https://drive.google.com/uc?export=view&id=1CRrP0yZZyVD-XV9McVopTPtRz7zgusXX">

 - cuDNN 확인, 다음 커맨드를 실행하여 버젼 확인

```
/sbin/ldconfig -N -v $(sed ‘s/:/ /’ <<< $LD_LIBRARY_PATH) 2>/dev/null | grep libcudnn
```

(2. 내용은 다음 [포스팅](https://medium.com/@stephengregory_69986/installing-cuda-10-1-on-ubuntu-20-04-e562a5e724a0)을 참고했다.)