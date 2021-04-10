---
layout: post
title: Pytorch의 유용한 기본 함수들 (expand, randperm, argmax, topk, sort, ones, zeros)
subheading: Tensor 첫 걸음
author: Jiyoung Min
categories: [Deeplearning]
tags: [tutorial, pytorch]
---

## Pytorch useful methods

- 이 포스팅에서는 빈번하게 사용될 수 있는 pytorch의 기본 함수에 대해 소개한다.   
- expand, randperm, argmax, topk, sort, ones, zeros에 대해 다뤄보고자 한다.

## 1. expand
- `.expande`는 텐서의 특정 dim을 복사하여 원하는 형태의 shape를 맞추는데 사용된다.

- 바로 broadcasting 하지 않고, 이렇게 expand를 한 후 연산을 하기도 한다.    
  의도하지 않는 broadcasting 연산으로 인한 오류를 막을 수 있다.

<u>[코드]</u>

```python
import torch

x = torch.FloatTensor([[[1, 2]],
                       [[3, 4]]])
print(x.size())
```
<u>[결과]</u>

    torch.Size([2, 1, 2])

***


<u>[코드]</u>

```python
y = x.expand((2, 3, 2)) # <-> *[2, 3, 2]

print(y)
print(y.size())
```
<u>[결과]</u>


    tensor([[[1., 2.],
             [1., 2.],
             [1., 2.]],
    
            [[3., 4.],
             [3., 4.],
             [3., 4.]]])
    torch.Size([2, 3, 2])

***


## 2. randperm
- random permutation
- 0부터 n까지의 숫자를 랜덤한 순서로 가진 텐서를 생성

<u>[코드]</u>

```python
x = torch.randperm(9)

print(x, x.size())
```
<u>[결과]</u>


    tensor([8, 5, 4, 6, 2, 1, 7, 0, 3]) torch.Size([9])

***


## 3. argmax
- maximum 값을 가지고 있는 index를 리턴한다.
- dim을 지정할 수 있다.
- dim이 감소한다. ex. (3,3,3) -> (3,3)
- **이미지**

<img src="https://drive.google.com/uc?export=view&id=1aNH5-w_5Ti1h8ETiTUZ_btn70MaLrQ2G">


<u>[코드]</u>

```python
x = torch.randperm(3**3).reshape(-1, 3, 3)

print(x, x.size())
```
<u>[결과]</u>


    tensor([[[ 1, 15,  3],
             [10, 25, 13],
             [11, 26, 20]],
    
            [[17,  2,  7],
             [ 6, 16, 22],
             [18, 23,  9]],
    
            [[14,  4,  0],
             [24, 21, 19],
             [12,  8,  5]]]) torch.Size([3, 3, 3])

***


<u>[코드]</u>

```python
y = x.argmax(dim=0)

print(y, y.size())
```
<u>[결과]</u>


    tensor([[1, 0, 1],
            [2, 0, 1],
            [1, 0, 0]]) torch.Size([3, 3])

***


<u>[코드]</u>

```python
y = x.argmax(dim=1)

print(y, y.size())
```
<u>[결과]</u>


    tensor([[2, 2, 2],
            [2, 2, 1],
            [1, 1, 1]]) torch.Size([3, 3])

***


<u>[코드]</u>

```python
y = x.argmax(dim=-1)

print(y, y.size())
```
<u>[결과]</u>


    tensor([[1, 1, 1],
            [0, 2, 1],
            [0, 0, 0]]) torch.Size([3, 3])

***


## 4. topk
- Top k개의 value와 index를 리턴한다.
- dim을 지정할 수 있다.
- dim=-1로 지정할 경우, x텐서에 대한 결과의 size는 (x의 dim=0, x의 dim=1, k)
- k=1이더라도, dim이 감소하지 않는다. ex. (3,3,3) -> (3,3,1)

<u>[코드]</u>

```python
values, indices = torch.topk(x, k=1, dim=-1)

print(x.size())
print(values.size())
print(indices.size())
```
<u>[결과]</u>


    torch.Size([3, 3, 3])
    torch.Size([3, 3, 1])
    torch.Size([3, 3, 1])

***


<u>[코드]</u>

```python
print("values:\n{}\n".format(values))
print("-----------------------------")
print("indices:\n{}\n".format(indices))
```
<u>[결과]</u>


    values:
    tensor([[[15],
             [25],
             [26]],
    
            [[17],
             [22],
             [23]],
    
            [[14],
             [24],
             [12]]])
    
    -----------------------------
    indices:
    tensor([[[1],
             [1],
             [1]],
    
            [[0],
             [2],
             [1]],
    
            [[0],
             [0],
             [0]]])
 
***
   


### topk vs. argmax
- k=1 이더라도 dim은 감소하지 않기 때문에, unsqueeze함수를 사용하여 감소시킬 수 있다.
- 이렇게 감소시킨 값은, dim을 감소시키는 argmax와 동일하게 된다.

<u>[코드]</u>

```python
print(values.squeeze(-1))
print(indices.squeeze(-1))
```
<u>[결과]</u>


    tensor([[15, 25, 26],
            [17, 22, 23],
            [14, 24, 12]])
    tensor([[1, 1, 1],
            [0, 2, 1],
            [0, 0, 0]])

***


<u>[코드]</u>

```python
print(x.argmax(dim=-1) == indices.squeeze(-1))
```
<u>[결과]</u>


    tensor([[True, True, True],
            [True, True, True],
            [True, True, True]])

***


- 또는 k가 2이상 일 때, 원하는 index를 지정해줄 수 있다.

<u>[코드]</u>

```python
_, indices = torch.topk(x, k=2, dim=-1)
print(indices.size())

print(x.argmax(dim=-1) == indices[:, :, 0])
```
<u>[결과]</u>


    torch.Size([3, 3, 2])
    tensor([[True, True, True],
            [True, True, True],
            [True, True, True]])

***


### sort by using topk
- topk를 이용하여 텐서를 sort할 수 있다.
- 아래 예시 코드를 통해, dim=-1 방향으로 크기가 큰 순서대로 정렬된 것을 볼 수 있다.   
  (15, 3, 1) , (25, 13, 10) , ...

<u>[코드]</u>

```python
target_dim = -1
values, indices = torch.topk(x,
                             k=x.size(target_dim),
                             largest=True)
print(values)
```
<u>[결과]</u>


    tensor([[[15,  3,  1],
             [25, 13, 10],
             [26, 20, 11]],
    
            [[17,  7,  2],
             [22, 16,  6],
             [23, 18,  9]],
    
            [[14,  4,  0],
             [24, 21, 19],
             [12,  8,  5]]])

***


## 5. sort
- 텐서를 원하는 dim에서 오름/내림 차순으로 정렬할 수 있다.
- 응용하여 topk처럼 사용할 수 있다.

<u>[코드]</u>

```python
values, indices = torch.sort(x, dim=-1, descending=True)

print(values)
```
<u>[결과]</u>


    tensor([[[15,  3,  1],
             [25, 13, 10],
             [26, 20, 11]],
    
            [[17,  7,  2],
             [22, 16,  6],
             [23, 18,  9]],
    
            [[14,  4,  0],
             [24, 21, 19],
             [12,  8,  5]]])

***


### topk by using sort
- 아래 코드는 `values, indices = torch.topk(x, k=1, dim=-1)`와 동일한 결과를 갖는다.

<u>[코드]</u>

```python
k=1
values, indices = torch.sort(x, dim=-1, descending=True)
values, indices = values[:, :, :k], indices[:, :, :k]

print(values)
print(indices)
```
<u>[결과]</u>


    tensor([[[15],
             [25],
             [26]],
    
            [[17],
             [22],
             [23]],
    
            [[14],
             [24],
             [12]]])
    tensor([[[1],
             [1],
             [1]],
    
            [[0],
             [2],
             [1]],
    
            [[0],
             [0],
             [0]]])

***


## 6. ones & zeros
- 원하는 shape를 0 또는 1로 채워넣는다.
- torch의 ones_like(x)와 zeros_like(x) 함수를 통해,   
  **x의 size, type, device를 동일하게 맞추어** 0또는 1을 생성할 수 있다.
- device를 맞춘다는 것은 생성될 텐서가 cpu 메모리 혹은 gpu 메모리 중 어디에 올릴지 또한 맞춰준다는 것이다.

<u>[코드]</u>

```python
print(torch.ones(2, 3))
print(torch.zeros(2, 3))
```
<u>[결과]</u>


    tensor([[1., 1., 1.],
            [1., 1., 1.]])
    tensor([[0., 0., 0.],
            [0., 0., 0.]])

***


<u>[코드]</u>

```python
x = torch.FloatTensor([[1, 2, 3],
                       [4, 5, 6]])
print(x.size())

print("----------------------------")

print(torch.ones_like(x))
print(torch.zeros_like(x))
```
<u>[결과]</u>


    torch.Size([2, 3])
    ----------------------------
    tensor([[1., 1., 1.],
            [1., 1., 1.]])
    tensor([[0., 0., 0.],
            [0., 0., 0.]])

***

이 포스팅은 패스트캠퍼스 김기현의 딥러닝 유치원 강의 기반으로 작성되었다.
