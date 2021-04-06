---
layout: post
title: 우분투(Ubuntu) 서버에 SSH 세팅
subheading: 딥러닝을 위한 서버 세팅 (3)
author: Jiyoung Min, Kyung Hyun Lee
categories: [Summary & Tips]
tags: [tutorial, server setting]
banner: https://cdn.arstechnica.net/wp-content/uploads/2019/11/ubuntu1910-desktop-1-1280x720.jpg
---

## 1. SSH 서비스 설치 및 설정하기

- 다음 명령어들은 root나 sudo 권한을 가지고 있는 user에서 수행할 수 있다.

### A. <u> SSH 원격접속이 가능하도록 설정하기 </u>

- 터미널에서 `openssh-server` 패키지 설치하기.

```
sudo apt update
sudo apt install openssh-server
```
<br/>

- 패키지가 설치되었다면, 자동으로 SSH service가 시작될 것이다. 성공적으로 설치되었는지 확인하기 위해 다음 커멘드를 실행해 본다.   
  `Active: active (running)`과 같은 문구가 보이면 성공적으로 작동하고 있는 것임을 알 수 있다.    
  q를 눌러 커멘드창으로 돌아올 수 있다.

```
sudo systemctl status ssh
```
<br/>

- `ip a` 커멘드를 통해 본인의 IP address를 확인할 수 있다.

    <img src="https://drive.google.com/uc?export=view&id=1TEKg_R9BDPnI5KsURwG8aOkd5DjXTK6d">

(1.A 내용은 다음 [포스팅](https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-18-04/)을 참고했다.)

### B. <u> SSH Port 변경하기 </u>

- 기본 포트는 default로 **22**로 설정되어 있다. 원하는 Port 번호로 변경할 수 있다.   
  다음 커멘드를 실행하고, 편집기에서 **# Port 22** 라고 입력되어 있는 줄을   
  `Port "your desired port"`로 변경해 주면 된다.   
  ex. `Port 8822`

- vim 사용법
  - sudo vim ~/.profile 이후, `i`를 입력하여 수정모드로 변환
  - 수정 후, `:wq!`를 입력하여 저장 후 종료하기

```
sudo vim /etc/ssh/sshd_config
```
<br/>

- 이제 다음 커멘드를 통해 ssh 서비스를 restart하면, 포트 변경 설정이 완료된다.

```
sudo service ssh restart
```


## 2. SSH 외부 IP, Port 설정하기

-  추가 예정