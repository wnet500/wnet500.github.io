---
layout: post
title: Pytorch Tensor의 기본 연산 (Operations)
subheading: Tensor 첫 걸음
author: Jiyoung Min
categories: [인공지능, 딥러닝]
tags: [pytorch, study]
---

##  Pytorch Tensor Operation
- 기본 사칙연산을 포함하는 기본 연산이 텐서에서 어떠한 식으로 이루어지는 아는 것은 매우 중요하다.


```python
import torch

a = torch.FloatTensor([[1, 2],
                       [3, 4]])
b = torch.FloatTensor([[2, 2],
                       [3, 3]])
```

## 1. Element-wise operations
- 덧셈, 뺏셈, 곱셈, 나눗셈 연산자 (`+, -, *, /`)
- 동등 비교 연산자 (`==, !=`)
- 제곱 연산자 (`**`)


```python
#----- 덧셈
print("덧셈 연산:\n{}\n".format(a + b))

#----- 뺄셈
print("뺄셈 연산:\n{}\n".format(a - b))

#----- 곱셈
print("곱셈 연산:\n{}\n".format(a * b))

#----- 나눗셈
print("나눗셈 연산:\n{}\n".format(a / b))

```
<u>[결과]</u>

    덧셈 연산:
    tensor([[3., 4.],
            [6., 7.]])
    
    뺄셈 연산:
    tensor([[-1.,  0.],
            [ 0.,  1.]])
    
    곱셈 연산:
    tensor([[ 2.,  4.],
            [ 9., 12.]])
    
    나눗셈 연산:
    tensor([[0.5000, 1.0000],
            [1.0000, 1.3333]])
    
***


## 2. Sum, Mean (Dimension Reducing Operations)
- 같은 shape의 텐서끼리 sum과 mean 연산을 수행하면, dimension이 줄어들게 된다.
- 어떤 dimension을 기준으로 연산을 할 지 정할 수도 있다.

<img src="https://drive.google.com/uc?export=view&id=1QBI6bTF9loocq7F84JO6o2E9h5nOi04D">

### 2차원 텐서

<u>[코드]</u>

```python
x = torch.FloatTensor([[1, 2],
                       [3, 4]])
print(x.sum())
print(x.mean())
```
<u>[결과]</u>

    tensor(10.)
    tensor(2.5000)
***


<u>[코드]</u>

```python
print(x.sum(dim=0))
print(x.mean(dim=0))
```
<u>[결과]</u>

    tensor([4., 6.])
    tensor([2., 3.])
***


### 3차원 텐서

<u>[코드]</u>

```python
x = torch.FloatTensor([[[1, 2, 2],
                        [3, 4, 4]],
                       [[5, 6, 6],
                        [7, 8, 8]],
                       [[9, 10, 10],
                        [11, 12, 12]]])
```

```python
print(x.sum(dim=0), x.size(), "\n")
print(x.sum(dim=1), x.size(), "\n")
print(x.sum(dim=2), x.size(), "\n") # <-> x.sum(dim=-1)
```
<u>[결과]</u>

    tensor([[15., 18., 18.],
            [21., 24., 24.]]) torch.Size([3, 2, 3]) 
    
    tensor([[ 4.,  6.,  6.],
            [12., 14., 14.],
            [20., 22., 22.]]) torch.Size([3, 2, 3]) 
    
    tensor([[ 5., 11.],
            [17., 23.],
            [29., 35.]]) torch.Size([3, 2, 3]) 
    
***


## 3. BoradCast in Operations
- 다른 shape를 가진 tensor끼리 연산을 가능하게 한다.   
  (dim이 낮은 텐서에서 dim을 높은 텐서에 맞춰 dim을 확장한 후 연산하는 원리)

- 모든 shape의 tensor끼리 연산이 가능한 것은 아니다.

### <u>Tensor + Scalar</u>

<u>[코드]</u>

```python
x = torch.FloatTensor([[1, 2],
                       [3, 4]])
y = 1
```

<u>[코드]</u>

```python
print(x + y)
```
<u>[결과]</u>

    tensor([[2., 3.],
            [4., 5.]])

***

### <u>Tensor + Vector</u>

<u>[코드]</u>

```python
 x = torch.FloatTensor([[1, 2],
                       [4, 8]])
y = torch.FloatTensor([3, 5])

print(x.size())
print(y.size())
```
<u>[결과]</u>

    torch.Size([2, 2])
    torch.Size([2])

***

<u>[코드]</u>

```python
z = x + y
print(z)
print(z.size())
```
<u>[결과]</u>

    tensor([[ 4.,  7.],
            [ 7., 13.]])
    torch.Size([2, 2])

***

### <u>Tensor + Tensor</u>

<u>[코드]</u>

```python
x = torch.FloatTensor([[1, 2]])
y = torch.FloatTensor([[3],
                       [5]])

print(x.size())
print(y.size())
```
<u>[결과]</u>

    torch.Size([1, 2])
    torch.Size([2, 1])

***

<u>[코드]</u>

```python
z = x + y
print(z)
print(z.size())
```
<u>[결과]</u>

    tensor([[4., 5.],
            [6., 7.]])
    torch.Size([2, 2])
***


위 수행 결과는 아래와 같이 이루어 진 것과 같다.

<u>[코드]</u>

```python
x = torch.FloatTensor([[1, 2],
                       [1, 2]])
y = torch.FloatTensor([[3, 3],
                       [5, 5]])
```


```python
z = x + y
print(z)
print(z.size())
```
<u>[결과]</u>

    tensor([[4., 5.],
            [6., 7.]])
    torch.Size([2, 2])

***
이 포스팅은 패스트캠퍼스 김기현의 딥러닝 유치원 강의 기반으로 작성되었다.

