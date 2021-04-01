---
layout: post
title: 마크다운(Markdown) 핵심 작성법
subheading: 쉽고 빠르게 글 작성하기
author: Jiyoung Min
categories: [Summary & Tips]
tags: [vscode, markdown]
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

