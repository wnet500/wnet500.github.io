---
layout: post
title: Pytorch Tensor shaping (reshape, squeeze, unsqueeze)
subheading: Tensor 첫 걸음
author: Jiyoung Min
categories: [Deeplearning]
tags: [tutorial, pytorch]
---

## Pytorch shaping
- 텐서의 shape를 변경할 수 있다.

- `reshape`, `squeeze`, `unsqueeze` 함수를 사용할 수 있다.

<u>[코드]</u>

```python
import torch

x = torch.FloatTensor([[[1, 2],
                        [3, 4]],
                       [[5, 6],
                        [7, 8]],
                       [[9, 10],
                        [11, 12]]])

print(x.size())
```
<u>[결과]</u>

    torch.Size([3, 2, 2])

***

## 1. reshape 함수
- -1은 "나머지 숫자는 알아서 계산해줘"라는 의미로 사용 가능하다.

<u>[코드]</u>

```python
#----- 두 연산의 결과 값은 같음
print(x.reshape(12)) # 3*2*2 = 12
print(x.reshape(-1))
```
<u>[결과]</u>


    tensor([ 1.,  2.,  3.,  4.,  5.,  6.,  7.,  8.,  9., 10., 11., 12.])
    tensor([ 1.,  2.,  3.,  4.,  5.,  6.,  7.,  8.,  9., 10., 11., 12.])

***

<u>[코드]</u>

```python
#----- 두 연산의 결과 값은 같음
print(x.reshape(3, 4)) # 3*4 = 12
print(x.reshape(3, -1)) 
```
<u>[결과]</u>


    tensor([[ 1.,  2.,  3.,  4.],
            [ 5.,  6.,  7.,  8.],
            [ 9., 10., 11., 12.]])
    tensor([[ 1.,  2.,  3.,  4.],
            [ 5.,  6.,  7.,  8.],
            [ 9., 10., 11., 12.]])

***

<u>[코드]</u>

```python
print(x.reshape(3, 1, 4))
print(x.reshape(-1, 1, 4))
```
<u>[결과]</u>


    tensor([[[ 1.,  2.,  3.,  4.]],
    
            [[ 5.,  6.,  7.,  8.]],
    
            [[ 9., 10., 11., 12.]]])
    tensor([[[ 1.,  2.,  3.,  4.]],
    
            [[ 5.,  6.,  7.,  8.]],
    
            [[ 9., 10., 11., 12.]]])

***


## 2. squeeze 함수
- 오직 1개의 element를 가지고 있는 dimension을 제거할 수 있다.
- 또한 제거할 dimensiond을 선택할 수 있다.

<u>[코드]</u>

```python
x = torch.FloatTensor([[[1, 2],
                        [3, 4]]])
print(x.size())
```
<u>[결과]</u>


    torch.Size([1, 2, 2])

***

<u>[코드]</u>

```python
print(x.squeeze())
print(x.squeeze().size())
```
<u>[결과]</u>


    tensor([[1., 2.],
            [3., 4.]])
    torch.Size([2, 2])

***


- 제거할 dim을 선택할 수 있으며, 만약 선택한 dim이 element를 한 개 가지고 있는 것이 아니면, 아무 일도 일어나지 않는다.

<u>[코드]</u>

```python
print(x.squeeze(0), x.squeeze(0).size())
print()
print(x.squeeze(1).size()) # 아무 변화도 일어나지 않음
```
<u>[결과]</u>


    tensor([[1., 2.],
            [3., 4.]]) torch.Size([2, 2])
    
    torch.Size([1, 2, 2])

***


## 3. unsqueeze 함수
- 원하는 dim 자리에 dim을 추가할 수 있다.

<u>[코드]</u>

```python
x = torch.FloatTensor([[1, 2],
                       [3, 4]])
print(x.size())
```
<u>[결과]</u>


    torch.Size([2, 2])

***

<u>[코드]</u>

```python
z = x.unsqueeze(0)
print(z, z.size())

print("-------------------------------------------\n")

z = x.unsqueeze(-1)
print(z, z.size())
```
<u>[결과]</u>


    tensor([[[1., 2.],
             [3., 4.]]]) torch.Size([1, 2, 2])
    -------------------------------------------
    
    tensor([[[1.],
             [2.]],
    
            [[3.],
             [4.]]]) torch.Size([2, 2, 1])

***

이 포스팅은 패스트캠퍼스 김기현의 딥러닝 유치원 강의 기반으로 작성되었다.