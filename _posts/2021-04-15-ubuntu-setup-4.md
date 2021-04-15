---
layout: post
title: 우분투(Ubuntu) 서버에 여러 버전의 CUDA와 cuDNN 설치
subheading: 최신 pytorch와 tensorflow를 동시에 사용하기
author: Jiyoung Min, Kyung Hyun Lee
categories: [리눅스 서버, 인공지능 & 딥러닝]
tags: [tips, server setting, tensorflow, pytorch]
banner: https://res.cloudinary.com/practicaldev/image/fetch/s--5Epkp0zJ--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://www.tipard.com/images/video/cuda.jpg
---

## 1. 여러 버전의 CUDA와 cuDNN 필요성

- 보통 파이썬으로 딥러닝을 구현하는데 개발자에 따라 메인으로 쓰는 프레임워크가 있다. `Pytorch 또는 `Tensorflow`가 가장 많이 쓰이는 프레임워크이다.

- 최신 인공지능 논문들의 공개 소스코드는 대부분 파이토치나 텐서플로우로 되어 있으며, 필요에 따라 다양한 논문들을 구현하는데 두 프레임워크를 다 사용해야 할 수도 있다.

- 하지만, 현재 (2021-04-15 기준) 최신 파이토치와 텐서플로우는 서로 다른 cuda 버젼 위에서 작동한다.   
  <u>Pytorch의 경우 cuda 11.1</u>, <u>Tensorflow의 경우 cuda 11.0</u>을 지원한다.

## 2. 준비 사항

- 우분투 서버

- 이전 포스팅 [우분투(Ubuntu) 서버에 CUDA와 cuDNN 설치](https://wnet500.github.io/%EB%A6%AC%EB%88%85%EC%8A%A4%20%EC%84%9C%EB%B2%84/2021/04/04/ubuntu-setup-1.html)를 보고 온다.

## 3. 여러 버전의 CUDA toolkit & cuDNN 설치

### A. <u>CUDA PPA 셋업</u>   

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

### B. <u>CUDA 패키지 다운로드 (cuDNN 라이브러리 포함)</u>

- CUDA 설치 버젼 결정 (2021-04-15 기준)

  - pytorch의 경우 cuda 11.1
    [여기](https://pytorch.org/)에서 설치 가능한 CUDA 버젼 확인 및 선택

  - tensorflow의 경우 cuda 11.0
    [여기](https://www.tensorflow.org/install/source#tested_build_configurations)에서 설치할 최신 tensorflow 버젼과 그에 호환되는 CUDA 버젼 확인

- cuDNN 버젼 결정
  - CUDA와 cuDNN의 compatibility를 [여기](https://docs.nvidia.com/deeplearning/cudnn/support-matrix/index.html)에서 확인
  - cuda 11.0과 11.1의 경우 cuDNN 8.0.0 ~ 8.0.1 버젼이 서로 호환된다.   
    (같은 cuDNN 버젼을 가지고 있어 설치가 수월해 졌다.)

- CUDA & cuDNN 설치
  - `sudo apt install cuda-"버젼"`, 11.1일 경우 버젼에 11-1 입력  
  - `sudo apt install libcudnn"Major 버젼"`, cuDNN 8.x.x버젼이 필요하므로, Major 버젼에 8 입력

```
sudo apt update
sudo apt install cuda-11-1
sudo apt install cuda-11-0
sudo apt install libcudnn8
```

- 잘 설치가 되었으면, `/usr/local` 경로에, <u>cuda, cuda-11.0, cuda-11.1 폴더가 생성된 것을 확인할 수 있다.</u>

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
  - 수정 후, esc를 누르고 `:wq!`를 입력하여 저장 후 종료하기

<br/>

- 마지막 줄에 다음 라이센스 코드를 추가
  - 아래 코드에서 보이는 코드에서, cuda 버젼에 따라 모든 "cuda-xx.x"을 알맞게 수정하기   
    이 포스팅에서는 cuda 11.1을 사용하므로, "cuda-11.1"을 사용

- 간단하게 cuda-11.0을 사용해보고, 안맞으면 cuda-11.1을 사용하라는 명령이다.
```
# set CUDA PATH
export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}

export LD_LIBRARY_PATH="/usr/local/cuda-11.0/lib64:/usr/local/cuda-11.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}"
```


## 4. Pytorch와 Tensorflow 실행

### A. <u>Pytorch 설치</u>   

- 파이토치 홈페이지 (https://pytorch.org/)에서 본인의 CUDA 버젼 및 세팅에 맞게 선택 후, 아래에서 실행할 command 얻기  
<br/>

    <img src="https://drive.google.com/uc?export=view&id=1hHutqTDZzTJTxRsCG_Fksk9gebuh12GX">

- 글쓴이의 경우 pytorch를 위해 생성해둔 가상환경에서 아래 커멘드를 실행하였다.    

```
pip install torch==1.8.1+cu111 torchvision==0.9.1+cu111 torchaudio==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
```

- `ipython` 커맨드를 입력한 후 `import torch`를 실행할 경우 다음과 같은 화면을 확인할 수 있다.

    <img src="https://drive.google.com/uc?export=view&id=1BnFuh7CkYa2q-qZtN11pSLEN2aNH22B_">


### B. <u>Tensroflow 설치</u> 

- 3.B에서 결정한 tensorflow 버젼 설치
  이 포스팅에서는 2.4.0 버젼을 선택

```
pip install tensroflow==2.4.0
```

- `ipython` 커맨드를 입력한 후 `import tensorflow as tf`를 실행할 경우 다음과 같은 화면을 확인할 수 있다.

    <img src="https://drive.google.com/uc?export=view&id=1_1K1PUsW4_rzaHVWUWMwBSamdkxhd85V">


- 다음 커맨드를 통해, 사용가능한 GPU 갯수를 확인할 수 있다.

```
tf.distribute.MirroredStrategy()

print ('Number of devices: {}'.format(tf.distribute.MirroredStrategy().num_replicas_in_sync))
```