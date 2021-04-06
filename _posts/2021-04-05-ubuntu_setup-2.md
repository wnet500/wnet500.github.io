---
layout: post
title: 우분투(Ubuntu) 서버에 SSH 세팅
subheading: 딥러닝을 위한 서버 세팅
author: Jiyoung Min, Kyung Hyun Lee
categories: [Summary & Tips]
tags: [tutorial, server setting]
banner: https://cdn.arstechnica.net/wp-content/uploads/2019/11/ubuntu1910-desktop-1-1280x720.jpg
---

## 1. 서버에 Ubuntu 20.04 설치
- 부팅 디스크를 만들어서 설치 (Ubuntu 20.04 버젼)


## 2. Chrome 설치 (선택 사항) 
- 파이어 폭스에서 Chrome 설치파일 다운로드
- 다운로드 폴더에서 다운된 파일 더블 클릭하여 설치하기


## 3. Ubuntu에 유저 생성하고 sudo 권한 주기

### A. <u> 유저 생성하기 </u>

- Ubuntu를 설치하고, root계정으로 위와 같은 GPU와 딥러닝 프레임워크 사용을 위한 세팅이 끝났으면, 새로운 유저 아이디를 만들어 사용하는 것이 좋다.
  다음 커멘드를 통해 유저 아이디 생성하자

- 아래 커멘드에서 "newuser"를 실제 유저가 사용할 아이디로 변경해 주자   
  ex. sudo adduser wnet500

- Full Name, Work phone, Other에 이메일 주소를 입력하게 하여 유저를 인식하고 관리하기 편하게 하면 좋다.

```
sudo adduser "newuser"
```

![](https://phoenixnap.com/kb/wp-content/uploads/2019/03/creating-sudo-user-ubuntu1.png)

### B. <u> 유저에게 sudo 권한 부여하기 </u>

- 관리자 유저에게 sudo 권한을 주어 전반적인 관리를 가능하게 할 수 있다. 다음 커멘드를 통해 sudo group에 해당 유저를 추가해 주자

```
sudo usermod -aG sudo "newuser"
```

(3. 내용은 다음 [포스팅](https://phoenixnap.com/kb/how-to-create-sudo-user-on-ubuntu)을 참고했다.)


## 4. SSH 설정하기

### A. <u> SSH 원격접속이 가능하도록 설정하기 </u>

- 터미널에서 `openssh-server` 패키지 설치하기.

```
sudo apt update
sudo apt install openssh-server
```
<br/>

- 패키지가 설치되었다면, 자동으로 SSH service가 시작될 것이다. 성공적으로 설치되었는지 확인하기 위해 다음 커멘드를 실행해 본다.   
  `Active: active (running)`과 같은 문구가 보이면 성공적으로 작동하고 있는 것임을 알 수 있다. q를 눌러 커멘드창으로 돌아올 수 있다.

```
sudo systemctl status ssh
```
<br/>

- `ip a` 커멘드를 통해 본인의 IP address를 확인할 수 있다.

    <img src="https://drive.google.com/uc?export=view&id=1TEKg_R9BDPnI5KsURwG8aOkd5DjXTK6d">

(4.A 내용은 다음 [포스팅](https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-18-04/)을 참고했다.)

### B. <u> SSH Port 변경하기 </u>

- 기본 포트는 default로 **22**로 설정되어 있다. 원하는 Port 번호로 변경할 수 있다.   
  다음 커멘드를 실행하고, 편집기에서 `# Port 22` 라고 입력되어 있는 줄을   
  `Port "your desired port"`로 변경해 주면 된다.   
  ex. `Port 8822`

```
sudo vim /etc/ssh/sshd_config
```
<br/>

- 이제 다음 커멘드를 통해 ssh 서비스를 restart하면, 포트 변경 설정이 완료된다.

```
sudo service ssh restart
```


## 5. SSH 외부 IP, Port 설정하기

-  추가 예정