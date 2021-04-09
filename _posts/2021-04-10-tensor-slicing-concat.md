---
layout: post
title: Pytorch Tensor 인덱싱(indexing), 연결(concatenation)
subheading: Tensor 첫 걸음
author: Jiyoung Min
categories: [Deeplearning]
tags: [tutorial, pytorch]
---

## Pytorch Tensor slicing & concatenation
- 인공지능을 학습 시킬 때, 목적에 따라 데이터셋과 네트워크 구조를 원하는대로 다루는 것은 중요하다.
- 이 포스팅은 Tensor를 자르고 붙이는 방법에 대해 정리해 보았다.

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

## 1. Indexing
### numpy 문법
- numpy와 같은 방법으로 인덱싱이 가능하다.

<u>[코드]</u>

```python
print(x[0])
print(x[0, :])
print(x[0, :, :])
```
<u>[결과]</u>


    tensor([[1., 2.],
            [3., 4.]])
    tensor([[1., 2.],
            [3., 4.]])
    tensor([[1., 2.],
            [3., 4.]])
***

<u>[코드]</u>

```python
print(x[:, :1, :].size())
print(x[:, :-1, :].size())
```
<u>[결과]</u>


    torch.Size([3, 1, 2])
    torch.Size([3, 1, 2])
***

- 단순히 데이터 1개를 얻는 것 뿐만 아니라, range를 통해 연속된 데이터를 얻을 수 있다.

- `a:b` 는 **a 이상 b 미만**을 의미한다.
- (ex.) 1:3 -> 1, 2   
  (ex.)  :-1 -> 0, 1, 2, ... ,-2 (마지막을 뺀 나머지) 

<u>[코드]</u>
```python
print(x[1:3, :, :], x[1:3, :, :].size())
```
<u>[결과]</u>


    tensor([[[ 5.,  6.],
             [ 7.,  8.]],
    
            [[ 9., 10.],
             [11., 12.]]]) torch.Size([2, 2, 2])
***

#### index_select
-  중복 추출이 가능하다.

<u>[코드]</u>

```python
x = torch.FloatTensor([[[1, 1],
                        [2, 2]],
                       [[3, 3],
                        [4, 4]],
                       [[5, 5],
                        [6, 6]]])
indices = torch.LongTensor([1, 0])

print(x.size())
```
<u>[결과]</u>


    torch.Size([3, 2, 2])
***

<u>[코드]</u>

```python
y = x.index_select(dim=0, index=indices)

print(y, y.size())
```
<u>[결과]</u>


    tensor([[[3., 3.],
             [4., 4.]],
    
            [[1., 1.],
             [2., 2.]]]) torch.Size([2, 2, 2])
***

<u>[코드]</u>

```python
y = x.index_select(dim=1, index=indices)

print(y, y.size())
```
<u>[결과]</u>


    tensor([[[2., 2.],
             [1., 1.]],
    
            [[4., 4.],
             [3., 3.]],
    
            [[6., 6.],
             [5., 5.]]]) torch.Size([3, 2, 2])
***

<u>[코드]</u>

```python
y = x.index_select(dim=-1, index=indices)

print(y, y.size())
```
<u>[결과]</u>


    tensor([[[1., 1.],
             [2., 2.]],
    
            [[3., 3.],
             [4., 4.]],
    
            [[5., 5.],
             [6., 6.]]]) torch.Size([3, 2, 2])
***

## 2. Spliting
- `split`과 `chunk`함수를 통해 텐서를 원하는 대로 분리할 수 있다. 다소 헷갈리는 개념이니 확실히 짚고 넘어가면 좋다.

- `split`은 **n개씩 묶어서** 분리한다.   
   마지막, n개보다 작은 묶음은 그대로 둔다.

- `chunck`는 **m 묶음으로** 분리한다.   
   마지막, 남은 묶음은 작은 묶음은 그대로 둔다.


<u>[코드]</u>

```python
x = torch.FloatTensor(range(30)).reshape(5,3,2)
print(x)
```
<u>[결과]</u>


    tensor([[[ 0.,  1.],
             [ 2.,  3.],
             [ 4.,  5.]],
    
            [[ 6.,  7.],
             [ 8.,  9.],
             [10., 11.]],
    
            [[12., 13.],
             [14., 15.],
             [16., 17.]],
    
            [[18., 19.],
             [20., 21.],
             [22., 23.]],
    
            [[24., 25.],
             [26., 27.],
             [28., 29.]]])
***

### split
- 2개씩 묶고, 마지막 1개는 그대로 둔다.

<u>[코드]</u>

```python
#----- split
splits = x.split(2, dim=0) # default dim = 0

for s in splits:
    print(s, s.size(), "\n----------------------------------")
```
<u>[결과]</u>


    tensor([[[ 0.,  1.],
             [ 2.,  3.],
             [ 4.,  5.]],
    
            [[ 6.,  7.],
             [ 8.,  9.],
             [10., 11.]]]) torch.Size([2, 3, 2]) 
    ----------------------------------
    tensor([[[12., 13.],
             [14., 15.],
             [16., 17.]],
    
            [[18., 19.],
             [20., 21.],
             [22., 23.]]]) torch.Size([2, 3, 2]) 
    ----------------------------------
    tensor([[[24., 25.],
             [26., 27.],
             [28., 29.]]]) torch.Size([1, 3, 2]) 
    ----------------------------------
***

### chunk
- 총 2묶음으로 묶기 위해 3개, 2개로 묶는다. (묶음: 큰 수 -> 작은 수)

<u>[코드]</u>

```python
#----- chunk
chunks = x.chunk(2, dim=0) # default dim = 0

for c in chunks:
    print(c, c.size(), "\n----------------------------------")
```
<u>[결과]</u>


    tensor([[[ 0.,  1.],
             [ 2.,  3.],
             [ 4.,  5.]],
    
            [[ 6.,  7.],
             [ 8.,  9.],
             [10., 11.]],
    
            [[12., 13.],
             [14., 15.],
             [16., 17.]]]) torch.Size([3, 3, 2]) 
    ----------------------------------
    tensor([[[18., 19.],
             [20., 21.],
             [22., 23.]],
    
            [[24., 25.],
             [26., 27.],
             [28., 29.]]]) torch.Size([2, 3, 2]) 
    ----------------------------------
***

- `dim=1`일 때, 두 번째 dim을 쪼갠다.

<u>[코드]</u>

```python
chunks = x.chunk(2, dim=1) # default dim = 0

print("x size:")
print(x.size(), "\n-----------------------------------")

print("chucked sizes:")
for c in chunks:
    print(c.size())
```
<u>[결과]</u>


    x size:
    torch.Size([5, 3, 2]) 
    -----------------------------------
    chucked sizes:
    torch.Size([5, 2, 2])
    torch.Size([5, 1, 2])
***

## 3. Concatenate & Stack
- `cat`과 `stack` 함수를 사용하여 여러 개의 텐서를 이어 붙이고 쌓을 수 있다.
- `cat`을 이용하여 여러 개의 텐서를 붙일 수 있다. (dim 변화 없음)
- `stack`을 이용하여 여러 개의 텐서를 쌓아 올릴 수 있다. (dim 변화 있음)

<img src="https://drive.google.com/uc?export=view&id=13QUyBx3_fz_L4v7YMNq17oV6x1ouBSIU">

<u>[코드]</u>

```python
x = torch.FloatTensor([[1, 2, 3],
                       [4, 5, 6],
                       [7, 8, 9]])
y = torch.FloatTensor([[10, 11, 12],
                       [13, 14, 15],
                       [16, 17, 18]])

print(x.size(), y.size())
```
<u>[결과]</u>


    torch.Size([3, 3]) torch.Size([3, 3])
***

### cat (차원 유지)

<u>[코드]</u>

```python
z = torch.cat([x, y], dim=0) # default dim = 0

print(z, z.size())
```
<u>[결과]</u>


    tensor([[ 1.,  2.,  3.],
            [ 4.,  5.,  6.],
            [ 7.,  8.,  9.],
            [10., 11., 12.],
            [13., 14., 15.],
            [16., 17., 18.]]) torch.Size([6, 3])
***

<u>[코드]</u>

```python
z = torch.cat([x, y], dim=1)

print(z, z.size())
```
<u>[결과]</u>


    tensor([[ 1.,  2.,  3., 10., 11., 12.],
            [ 4.,  5.,  6., 13., 14., 15.],
            [ 7.,  8.,  9., 16., 17., 18.]]) torch.Size([3, 6])
***

### stack (차원 증가)


```python
z = torch.stack([x, y], dim=0) # default dim = 0

print(z, z.size())
```
<u>[결과]</u>


    tensor([[[ 1.,  2.,  3.],
             [ 4.,  5.,  6.],
             [ 7.,  8.,  9.]],
    
            [[10., 11., 12.],
             [13., 14., 15.],
             [16., 17., 18.]]]) torch.Size([2, 3, 3])
***

<u>[코드]</u>

```python
z = torch.stack([x, y], dim=1)

print(z, z.size())
```
<u>[결과]</u>


    tensor([[[ 1.,  2.,  3.],
             [10., 11., 12.]],
    
            [[ 4.,  5.,  6.],
             [13., 14., 15.]],
    
            [[ 7.,  8.,  9.],
             [16., 17., 18.]]]) torch.Size([3, 2, 3])
***

<u>[코드]</u>

```python
z = torch.stack([x, y], dim=2)

print(z, z.size())
```
<u>[결과]</u>


    tensor([[[ 1., 10.],
             [ 2., 11.],
             [ 3., 12.]],
    
            [[ 4., 13.],
             [ 5., 14.],
             [ 6., 15.]],
    
            [[ 7., 16.],
             [ 8., 17.],
             [ 9., 18.]]]) torch.Size([3, 3, 2])
***

### 유용한 예제
- 리스트에 차곡차곡 쌓은 후, stack을 통해서 차원을 늘려 데이터셋을 구성할 수 있다.

<u>[코드]</u>

```python
w = [] + [torch.FloatTensor([1, 2])] + [torch.FloatTensor([3, 4])]
print(w)

print("\n-----------------------\n")

w = torch.stack(w)
print(w, w.size())
```
<u>[결과]</u>


    [tensor([1., 2.]), tensor([3., 4.])]
    
    -----------------------
    
    tensor([[1., 2.],
            [3., 4.]]) torch.Size([2, 2])

***
<u>[코드]</u>

```python
result = []
for i in range(5):
    x = torch.FloatTensor(2, 2)
    result += [x]

result = torch.stack(result)
result.size()
```
<u>[결과]</u>


    torch.Size([5, 2, 2])

***

이 포스팅은 패스트캠퍼스 김기현의 딥러닝 유치원 강의 기반으로 작성되었다.

