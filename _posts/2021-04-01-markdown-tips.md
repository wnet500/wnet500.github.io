---
layout: post
title: 마크다운(Markdown) 핵심 작성법 A-Z
date: 2021-04-01 20:12 +0800
tags: [jekyll theme, jekyll, tutorial]
toc:  true
---

## 1. 글씨/문장 강조

* 이텔릭(Italic) 
* 굴은 글씨(Bold)
* 모노스페이스(Monospace)
* 라인 블럭(Line block)

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



## 2. 헤더 (Header)

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


## 3. 목록 만들기

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



들여쓰기도 가능하다.
```
* 들여쓰기 1
    * 들여쓰기 2
        * 들여쓰기 3
```
* 들여쓰기 1
    * 들여쓰기 2
        * 들여쓰기 3



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



## 4. 블럭 인용문자 (Block quote)

```
> 이것은 첫 번째 블럭 인용문자 입니다.
>> 이것은 두 번째 블럭 인용문자 입니다.
>>> 이것은 세 번째 블럭 인용문자 입니다.
```

> 이것은 첫 번째 블럭 인용문자 입니다.

>> 이것은 두 번째 블럭 인용문자 입니다.

>>> 이것은 세 번째 블럭 인용문자 입니다.



**(Tip)** 블럭 인용문자 안에 마크다운의 다른 요소를 함께 사용할 수 있다.
> ##### 블럭 인용문자와 헤더 5

>> ``` 
>> 블럭 인용문자와 코드 블럭
>> ```



## 5. 코드 블럭 (Code block)

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



* 코드 블럭 행에 숫자를 부여할 수 있다.
    * {% highlight 언어 이름 linenos %}   
      코드 바디
      {% endhighlight %}
    * 위와 같은 형식으로 작성하면 된다. 언어 이름에는 python, javascript등이 사용될 수 있다.


{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}



## 6. 수평선 규칙 (Horizontal rule, (줄임말) HR.)

수평선은 주로 글의 섹션을 나눌 때 사용한다.
`***` 외에 여러 가지 방법이 있으나, 이것을 사용하는 것을 추천한다.

```
***
```

수평선 예시
* * *


## 7. 링크 연결

* 링크를 한 번만 사용할 경우 추천
    * 링크의 이름을 생략하고 `(링크)` 만 사용할 수 있다. 

```
문법: [제목](링크)

예시 1: [Google](https://google.com, "google link")
예시 2: [Google](https://google.com)
```

[Google](https://google.com, "google link")   
[Google](https://google.com)   



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

* URL에 직접 링크 연결

```
이 블로그의 주소: <https://wnet500.github.io/>
작성자 지영이의 이메일: <wnet50094@gmail.com>
```

이 블로그의 주소: <https://wnet500.github.io/>     
작성자 지영이의 이메일: <wnet50094@gmail.com>



## 8. 이미지 삽입

* 마크다운을 작성하는 워킹디렉토리에 있는 이미지 path를 사용할 수 있다.
    * 제목과, optional title은 생략 가능하다.

```
문법: ![제목](img path, "optional title")

![myhome bg](/bg.jpeg "mybg")
```

![myhome bg](/bg.jpeg "mybg")


* 이미지가 있는 URL 링크를 삽입할 수 있다.
    * 구글에서 이미지를 찾은 후, 마우스 우클릭 "이미지 주소 복사"를 클릭하면, URL링크를 얻을 수 있다.
    * 이 글에서는 URL: https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg 을 사용했다.
    * optional title은 생략할 수 있다.

```
문법: ![제목](img URL, "optional title")

![](https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg)
```
![](https://s3-ap-southeast-2.amazonaws.com/geg-gug-webapp/images/1557364192-work_while_you_study_banner.jpg)

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


## 9. 유튜브 동영상 삽입

```
문법 1: [![제목(생략가능)](https://img.youtube.com/vi/"유튜브 아이디"/0.jpg)]([유튜브 URL](https://www.youtube.com/watch?v="유튜브 아이디"))

예시 : [![](https://img.youtube.com/vi/UmX4kyB2wfg/0.jpg)](https://www.youtube.com/watch?v=UmX4kyB2wfg)
```

[![](https://img.youtube.com/vi/UmX4kyB2wfg/0.jpg)](https://www.youtube.com/watch?v=UmX4kyB2wfg)



## 10. 기본 표 만들기

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