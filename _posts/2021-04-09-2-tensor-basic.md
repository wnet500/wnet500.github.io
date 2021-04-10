---
layout: post
title: Pytorch Tensor 기본 개념 (type, shape, etc.)
subheading: Tensor 첫 걸음
author: Jiyoung Min
categories: [Deeplearning]
tags: [tutorial, pytorch]
---

## Tensor allocation
- `FloatTensor`: 실수

- `LongTensor`: 정수 값 이라고 생각하면 편하다, 주로 **인덱스** 값을 담기 위해 쓰인다.

- `ByteTensor`: 0과 1값을 담을 때 사용한다.

- `BoolTensor`: True와 False를 담을 때 사용한다.

<u>[코드]</u>

```python
import torch

#----- FloatTensor
ft = torch.FloatTensor([[1, 2],
                        [3, 4]])
print("FloatTensor:\n{}\n".format(ft))

#----- LongTensor
lt = torch.LongTensor([[1, 2],
                        [3, 4]])
print("LongTensor:\n{}\n".format(lt))

#----- ByteTensor
bt = torch.ByteTensor([[1, 0],
                        [0, 1]])
print("ByteTensor:\n{}\n".format(bt))

#----- BoolTensor
boolt = torch.BoolTensor([[1, 0],
                          [0, 1]])
print("BoolTensor:\n{}\n".format(boolt))
```
<u>[결과]</u>

    FloatTensor:
    tensor([[1., 2.],
            [3., 4.]])
    
    LongTensor:
    tensor([[1, 2],
            [3, 4]])
    
    ByteTensor:
    tensor([[1, 0],
            [0, 1]], dtype=torch.uint8)
    
    BoolTensor:
    tensor([[ True, False],
            [False,  True]])
    

***

## Tensor and Numpy Compatibility

- Numpy와 Tensor 사이의 자유로운 호환이 가능하다.

- `from_numpy(x)`: numpy -> tensor 변환

- `.numpy()`: tensor -> numpy 변환

<u>[코드]</u>

```python
import torch
import numpy as np 

#----- numpy array 정의
x = np.array([[1, 2],
              [3, 4]])
print(x, type(x), "\n")

#----- numpy -> tensor
y = torch.from_numpy(x)
print(y, type(y), "\n")

#----- tensor -> numpy
z = y.numpy()
print(z, type(z), "\n")
```
<u>[결과]</u>

    [[1 2]
     [3 4]] <class 'numpy.ndarray'> 
    
    tensor([[1, 2],
            [3, 4]]) <class 'torch.Tensor'> 
    
    [[1 2]
     [3 4]] <class 'numpy.ndarray'> 
    
***


## Type casting
- tensor의 type을 쉽게 변환할 수 있다.

- `.long()`, `.float()`,`.byte()`, `.bool()` 사용

<u>[코드]</u>

```python
print("FloatTensor -> LongTensor: \n{}\n".format(ft.long()))

print("LongTensor -> FloatTensor: \n{}\n".format(lt.float()))

print("FloatTensor-> ByteTensor: \n{}\n".format(torch.FloatTensor([1, 0]).byte()))

print("FloatTensor-> ByteTensor: \n{}\n".format(torch.FloatTensor([1, 0]).bool()))
```
<u>[결과]</u>

    FloatTensor -> LongTensor: 
    tensor([[1, 2],
            [3, 4]])
    
    LongTensor -> FloatTensor: 
    tensor([[1., 2.],
            [3., 4.]])
    
    FloatTensor-> ByteTensor: 
    tensor([1, 0], dtype=torch.uint8)
    
    FloatTensor-> ByteTensor: 
    tensor([ True, False])

***

    


## Get shape
- 다음 두 가지 방법을 통해 shape를 얻을 수 있다.
- `.size()`, `.shape`

<u>[코드]</u>

```python
x = torch.FloatTensor([[[1, 2],
                        [3, 4]],
                       [[5, 6],
                        [7, 8]],
                       [[9, 10],
                        [11, 12]]])
```


```python
print(x.size())
print(x.shape)
```
<u>[결과]</u>

    torch.Size([3, 2, 2])
    torch.Size([3, 2, 2])

***


<u>[코드]</u>

```python
#----- 0 번째 차원의 element 갯수
print(x.size(0))
print(x.shape[0])

#----- 마지막 차원의 element 갯수
print()
print(x.size(-1))
print(x.shape[-1])
```
<u>[결과]</u>

    3
    3
    
    2
    2

***


## Get number of dimensions
- 다음 두 가지 방법을 통해 차원의 갯수를 얻을 수 있다
- `.dim()`, `len(.size())`

<u>[코드]</u>

```python
print(x.dim())
print(len(x.size()))
```
<u>[결과]</u>

    3
    3

***


이 포스팅은 패스트캠퍼스 김기현의 딥러닝 유치원 강의 기반으로 작성되었다.