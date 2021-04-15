---
layout: post
title: 우분투(Ubuntu) 서버에 SSH 세팅
subheading: 딥러닝을 위한 서버 세팅 (3)
author: Jiyoung Min, Kyung Hyun Lee
categories: [리눅스 서버]
tags: [tutorial, server setting, ssh]
banner: https://cdn.arstechnica.net/wp-content/uploads/2019/11/ubuntu1910-desktop-1-1280x720.jpg
---

## 1. SSH 서비스 설치 및 설정하기

- 다음 명령어들은 root나 sudo 권한을 가지고 있는 user에서 수행할 수 있다.

### A. <u> SSH 원격접속이 가능하도록 설정하기 </u>

- 터미널에서 `openssh-server`와 `ssh` 패키지 설치하기

```
sudo apt update
sudo apt install openssh-server
sudo apt install ssh (or sudo apt-get install ssh)
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
  - 수정 후, esc를 누르고 `:wq!`를 입력하여 저장 후 종료하기

```
sudo vim /etc/ssh/sshd_config
```
<br/>

### C. UFW (uncomplicated Firewall) 설정하기

- 아래 커맨드를 실행하여 방화벽을 설정해준다.

```
sudo ufw enable
sudo ufw "your desired port"/tcp (ex. sudo ufw 8822/tcp)
```

- 이제 다음 커멘드를 통해 ssh 서비스를 restart하면, 포트 변경 설정이 완료된다.

```
sudo service ssh restart
```
### D. SSH 내부 원격접속하기

- 이제, 내부에서 서버와 같은 IP 뿌리를 가지고 있는 경우 (ex. 동일한 공유기 사용, 서버가 연결되어 있는 공유기의 wifi 사용) ssh 명령을 통해 서버에 접속할 수 있다.

```
ssh -p"your desired port" "ubuntu userid"@"server ip"

<예시>
ssh -p8822 testuser@101.101.0.1
```

## 2. SSH 외부 IP, Port 설정하기

-  1.의 설정을 끝내면, **내부 SSH**를 사용할 수 있다.   
   하지만, 학교 연구실이나 연구기관에 있는 서버를 그 공간에서만이 아닌 집이나 카페 등 다른 곳에서도 접속할 수 있으면 좋다. 

- iptime 공유기를 서버와 함께 사용하고 있는 경우 외부 SSH를 설정하는 방법에 대해 설명하고자 한다.

### A. 준비사항
1. iptime 공유기
2. 외부에서 사용하기 위해, SSH 포트포워딩에 사용할 외부 IP 정보와 방화벽을 해체한 port 할당받기   
   글쓴이의 경우 연구기관에 서버가 있으므로, 기관 IT부서에 신청하여 외부에 연결할 IP 정보와 port를 할당받았다. 

### B. 관리도구에 접속하기
- 서버 인터넷 url에 `192.168.0.1`을 입력한다.   
  admin으로 로그인 한다. 초기 비밀번호는 또한 admin으로 같다.

    <img src="https://drive.google.com/uc?export=view&id=123_inTBm5onYNj0OOSugyWsJSDvR_36L">

- 이후, `관리도구`를 선택한다.

### C. 포트포워드 설정하기

- `메뉴탐색기 > 고급 설정 > NAT/라우터관리 > 포트포워드 설정` 을 클릭한다.

- `새규칙 추가`를 누른 후 `규칙이름`을 원하는대로 입력해 준다. (ex. ssh_port_forwarding)

- 서버에서 관리도구에 접속했기 때문에, `현재 접속된 IP 주소`를 체크하였다.   
  (공유기에 연결된 다른 기기에서 접속했을 경우 공유기가 서버에 할당한 IP주소를 입력해준다, **1.A** 참고)

- 외부 포트와, 내부 포트를 입력한다.
  외부 포트는 할당받은 포트 입력, 내부 포트는 위에서 설정한 ssh 포트 번호 입력

- 이제 적용을 누르면, 외부 포트포워딩이 완료된다.

  <img src="https://drive.google.com/uc?export=view&id=1KGPSYFgf97dHz27EvlaY8Ld0WI8EuvAE">

- **(Tip)** `기본설정 > 시스템 요약 정보`에서 외부 IP 주소를 확인할 수 있다.

### D. 외부에서 서버에 접속하기

- 다음 커맨드를 통해 서버에 접속한다.

```
ssh -p"외부 포트" "ubuntu userid"@"외부 IP"

<예시>
ssh -p11004 testuser@211.106.133.164
```