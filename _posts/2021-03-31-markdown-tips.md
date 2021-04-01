---
layout: post
title: 마크다운(Markdown) 기본 작성법 정리
subheading: 쉽고 빠르게 마크다운을 이용해 글 작성하기
author: Jiyoung Min
categories: [Summary & Tips]
tags: [markdown, tutorial]
banner: https://blog.stephsmith.io/content/images/size/w2000/2019/10/joanna-kosinska-1_CMoFsPfso-unsplash-2-1.jpg
---

## 1. 마크다운(Markdown)

> 위키 백과에 따르면, 마크다운(markdown)은 일반 텍스트 기반의 경량 마크업 언어다.   
> 일반 텍스트로 서식이 있는 문서를 작성하는 데 사용되며, 일반 마크업 언어에 비해 문법이 쉽고 간단한 것이 특징이다.    
> HTML와 같은 서식 문서로 쉽게 변환되기 때문에 응용 소프트웨어와 함께 배포되는 README 파일이나 온라인 게시물 등에 많이 사용된다.

파일의 확장자는 md이며, 깃허브의 README.md가 대표적인 예시이다.   
이 블로그와 같이 깃허브 기반의 블로그를 작성하는데 필수적으로 필요한 언어이다.


## 2. 글씨/문장 강조

* 이텔릭(Italic) 
* 굴은 글씨(Bold)
* 모노스페이스(Monospace)
* 라인 블럭(Line block)
* 체크 박스(Task lists)

```
_이텔릭체 글씨_
*이텔릭체 글씨*

__굵은 글씨__
**굵은 글씨**

**_굵은 이텔릭체 글씨_**

~~취소선 글씨~~

`모노스페이스`

| 첫 번째 라인 블럭
| 두 번째 라인 블럭

- [x] 이것은 체크 박스 입니다.
- [ ] 이것은 비어있는 체크 박스 입니다.
```

_이텔릭체 글씨_    
*이텔릭체 글씨*


__굵은 글씨__   
**굵은 글씨** 


**_굵은 이텔릭체 글씨_**


~~취소선 글씨~~


`모노스페이스`


| 첫 번째 라인 블럭
| 두 번째 라인 블럭


- [x] 이것은 체크 박스 입니다.   
- [ ] 이것은 비어있는 체크 박스 입니다.


## 3. 헤더 (Header)

**(Tip)** `#` 6개 까지 지원한다.
이 블로그에서는 # 헤더 1이 사용되지 않는다.

```
## 헤더 2
### 헤더 3
#### 헤더 4
##### 헤더 5
###### 헤더 6
```

## 헤더 2
### 헤더 3
#### 헤더 4
##### 헤더 5
###### 헤더 6


## 4. 목록 만들기

```
1. 첫 번째 목록
2. 두 번째 목록
3. 세 번째 목록
```

1. 첫 번째 목록
2. 두 번째 목록
3. 세 번째 목록


```
* 첫 번째 글머리 기호
+ 두 번째 글머리 기호
- 세 번째 글머리 기호
```

* 첫 번째 글머리 기호
+ 두 번째 글머리 기호
- 세 번째 글머리 기호

<br/>

들여쓰기도 가능하다.
```
* 들여쓰기 1
    * 들여쓰기 2
        * 들여쓰기 3
```
* 들여쓰기 1
    * 들여쓰기 2
        * 들여쓰기 3

<br/>

**(Tip)** `*`, `+`, `-`를 혼합하여 사용할 수 있다.
```
* 들여쓰기 1
    + 들여쓰기 2
        - 들여쓰기 3
            - 들여쓰기 4
```

* 들여쓰기 1
    + 들여쓰기 2
        - 들여쓰기 3
            - 들여쓰기 4



## 5. 블럭 인용문자 (Block quote)

```
> 이것은 첫 번째 블럭 인용문자 입니다.
>> 이것은 두 번째 블럭 인용문자 입니다.
>>> 이것은 세 번째 블럭 인용문자 입니다.
```

> 이것은 첫 번째 블럭 인용문자 입니다.

>> 이것은 두 번째 블럭 인용문자 입니다.

>>> 이것은 세 번째 블럭 인용문자 입니다.

<br/>

**(Tip)** 블럭 인용문자 안에 마크다운의 다른 요소를 함께 사용할 수 있다.
> ##### 블럭 인용문자와 헤더 5

>> ``` 
>> 블럭 인용문자와 코드 블럭
>> ```



## 6. 코드 블럭 (Code block)

코드 블럭 코드 ``` 를 사용하여 나타낼 수 있다.

* 플레인텍스트 (Planetext)

````
```
이것은 코드 블럭 입니다.
```
````

```
이것은 코드 블럭 입니다.
```

<br/>

* python, javascript, markdown 등 언어를 선언하여, 실제 코드 문법처럼 나타낼 수 있다.

````
```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

p1 = Person("John", 36)

print(p1.name)
print(p1.age)
```
````

```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

p1 = Person("John", 36)

print(p1.name)
print(p1.age)
```

## 7. 수평선 규칙 (Horizontal rule)

수평선은 주로 글의 섹션을 나눌 때 사용한다.
`***` 외에 여러 가지 방법이 있으나, 이것을 사용하는 것을 추천한다.

```
***
```

수평선 예시
* * *


## 8. 링크 연결

* 링크를 한 번만 사용할 경우 추천
    * 링크의 이름을 생략하고 `(링크)` 만 사용할 수 있다. 

```
문법: [제목](링크)

예시 1: [Google](https://google.com, "google link")
예시 2: [Google](https://google.com)
```

[Google](https://google.com, "google link")   
[Google](https://google.com)   

<br/>

* 링크를 반복적으로 사용할 경우 추천
    * 마지막 줄에 사용한 링크를 정리한다.

```
문법: [제목][참조할 링크 이름]

예시:
유명한 사이트의 링크를 연결해보자.
먼저, [Google][google link]을 클릭하면 구글 사이트에 들어갈 수 있다.
[Google][google link]와 함께 유명한 사이트는 [Linkedin][linkedin link]이 있다.

[google link]: https://google.com
[linkedin link]: https://www.linkedin.com
```

유명한 사이트의 링크를 연결해보자.     
먼저, [Google][google link]을 클릭하면 구글 사이트에 들어갈 수 있다.     
[Google][google link]과 함께 유명한 사이트는 [Linkedin][linkedin link]이 있다.    

[google link]: https://google.com
[linkedin link]: https://www.linkedin.com

<br/>

* URL에 직접 링크 연결

```
이 블로그의 주소: <https://wnet500.github.io/>
작성자 지영이의 이메일: <wnet50094@gmail.com>
```

이 블로그의 주소: <https://wnet500.github.io/>     
작성자 지영이의 이메일: <wnet50094@gmail.com>



## 9. 이미지 삽입

* 마크다운을 작성하는 워킹디렉토리에 있는 이미지 path를 사용할 수 있다.
    * 제목과 optional title은 생략할 수 있다.
    * 이 글에서 해당 예시는 생략한다.

```
문법: ![제목](img path, "optional title")
```
<br/>

* 이미지가 있는 URL 링크를 삽입할 수 있다.
    * 구글에서 이미지를 찾은 후, 마우스 우클릭 "이미지 주소 복사"를 클릭하면, URL링크를 얻을 수 있다.
    * 이 글에서는 URL: https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg 을 사용했다.
    * 제목과 optional title은 생략할 수 있다.

```
문법: ![제목](img URL, "optional title")

예시:
![](https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg)
```
![](https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg)

<br/>

* 이미지 사이즈 변경
    * 이미지 사이즈를 변경하는 것은 조금 더 복잡하다.   
      직접 가로, 세로의 px값이나 크기 %를 설정해 주어야 한다.

```
문법:
<img src="이미지 path 또는 URL" width="숫자px 또는 숫자%" height="숫자px 또는 숫자%" title="제목" alt="사진 제목"></img>

예시 1:
<img src="https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg" width="400px" height="300px" title="이미지 사이즈 변경" alt="I Love MD"><br/>

예시 2:
<img src="https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg" width="50%" height="30%" title="이미지 사이즈 변경" alt="I Love MD">
```

<img src="https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg" width="350px" height="200px" title="이미지 사이즈 변경" alt="I Love MD"><br/>

<img src="https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg" width="45%" height="30%" title="이미지 사이즈 변경" alt="I Love MD">


## 10. 유튜브 동영상 삽입

* 마크다운 문법을 통해 링크 형식으로 다음과 같이 삽입할 수 있으나, 블로그 자체에서 동영상을 보기는 어렵다.


```
문법 1: [![제목(생략가능)](https://img.youtube.com/vi/"유튜브 아이디"/0.jpg)]([유튜브 URL](https://www.youtube.com/watch?v="유튜브 아이디"))

예시 : [![](https://img.youtube.com/vi/Ptk_1Dc2iPY/0.jpg)](https://www.youtube.com/watch?v=Ptk_1Dc2iPY)
```

[![](https://img.youtube.com/vi/Ptk_1Dc2iPY/0.jpg)](https://www.youtube.com/watch?v=Ptk_1Dc2iPY)

<br/>

* HTML 태그를 사용하여 블로그에서 직접 시청할 수 있는 유튜브 영상을 삽입할 수 있다.
  * 유튜브 동영상에서 마우스 우클릭하여 "소스 코드 복사" 이후, 붙여넣으면 된다.
  

```
예시 :
<iframe width="791" height="396" src="https://www.youtube.com/embed/Ptk_1Dc2iPY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

<iframe width="791" height="396" src="https://www.youtube.com/embed/Ptk_1Dc2iPY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## 11. 기본 표 만들기

```
| 첫 번째 컬럼 | 두 번째 컬럼 |
| --- | --- |
| 셀 1 | 셀 2 |
| 셀 3 | 셀 4 |
```

| 첫 번째 컬럼 | 두 번째 컬럼 |
| --- | --- |
| 셀 1 | 셀 2 |
| 셀 3 | 셀 4 |

<br/>

* 마크다운 기본 문법을 표 안에서 사용할 수 있다.

```
| 첫 번째 컬럼 | 두 번째 컬럼 |
| --- | --- |
| `셀 1` | *셀 2* |
| `셀 3` | **셀 4** |
```

| 첫 번째 컬럼 | 두 번째 컬럼 |
| --- | --- |
| `셀 1` | *셀 2* |
| `셀 3` | **셀 4** |

<br/>

* 각 열을 왼쪽, 가운데, 오른쪽 정렬을 할 수 있다.

```
| 왼쪽 정렬 | 가운데 정렬 | 오른쪽 정렬 |
| :--- | :---: | ---: |
| 왼쪽으로 | 가운데로 | 오른쪽으로 정렬합니다. |
| 정렬 | 정렬이 잘 될까? | 결과는? |
```

| 왼쪽 정렬 | 가운데 정렬 | 오른쪽 정렬 |
| :--- | :---: | ---: |
| 왼쪽으로 | 가운데로 | 오른쪽으로 정렬합니다. |
| 정렬 | 정렬이 잘 될까? | 결과는? |

***
이것으로 마크다운 핵심 작성법 포스팅을 마친다.
