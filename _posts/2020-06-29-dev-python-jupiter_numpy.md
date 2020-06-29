---
layout: post  
title: "[Python] Jupiter Notebook에서 numpy"  
subtitle: "쥬피터 노트북에서 넘파이의 사용"  
categories: dev
tags: python
comments: true
---

> 쥬피터 노트북에서 넘파이의 사용

# numpy


- 행렬 / 선형대수 / 통계 패키지

- 머신러닝의 이론적 백그라운드는 선형대수와 통계로 이루어져 있다

- 사이킷런 같은 머신러닝 패키지가 넘파이 기반으로 되어 있다


    * 머신러닝 알고리즘이나 사이파이와 같은 과학, 통계 지원용 패키지를 직접 만드는 개발이 아니라면
    넘파이를 상세하기 알 필요는 없다지만, 넘파이를 이해하는 것이 파이썬 기반의 데이타분석과 머신러닝에 중요하다
    
    * 넘파이가 데이타 핸들링에 효율적으로 쉽고 편하고 할 수 없다.
      그러나 데이타 핸들링에 주로 사용하는 판다스도 많은 부분이 넘파이를 기반으로 만들어져 있다.
    
    * ndarray 
        - 넘파이 기반 데이타 타입
        - np.array()       


```python
import numpy as np

list_1=[1,2,3]
list_2=[9,8,7]

arr =np.array([list_1,list_2])

print(type(arr)) # nd array

```

    <class 'numpy.ndarray'>



```python
arr.shape # 몇행 몇 열인지를 알려주는 것
```




    (2, 3)




```python
#두번째 행 두번째 열의 요소를 100으로 지정

arr[1][1]=100
arr
```




    array([[  1,   2,   3],
           [  9, 100,   7]])




```python
?arr # 도움말 부르기
```


```python
arr1=np.array([1,2,3])
arr2=np.array([[1,2,3]])

print(arr1.shape) # (3,) : 3개의 요소를 가지고 있는 튜플 이라는뜻
print(arr2.shape)

print(arr1.ndim,"차원")
print(arr2.ndim,"차원")
```

    (3,)
    (1, 3)
    1 차원
    2 차원


### 자료형


```python
print(arr.dtype)
```

    int32



```python
arr2=arr.astype(np.float64) # 실수형 사용할 때 뒤에 0붙는것을 생략하고 .만 씀
arr2
```




    array([[  1.,   2.,   3.],
           [  9., 100.,   7.]])




```python
list_3=[100,40,99,'python']
arr3=np.array(list_3)
print(type(arr3)) # 리스트의 자료형은 numpy.ndarray이다.
print(arr3.dtype) #안에 담긴 숫자는 int32이다.
 # < u32라는 형이나옴
```

    <class 'numpy.ndarray'>
    <U11



```python
  # [결과] <U11   : Unicode 문자열 
```

### nparray를 편리하게 생성

* arange() : 범위를 이용한 배열 만들기
* zeros() : 0으로 채우는 배열 만들기
* ones() : 1로 채우는 배열 만들기


```python
a= np.arange(10)
a
b=np.arange(1,11)
b
c=np.arange(1,11,3)
c
```




    array([ 1,  4,  7, 10])




```python
a2=np.zeros((5,5),dtype='int32')
a2
```




    array([[0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0]])




```python
a3=np.ones((4,4),dtype='int32')
a3
```




    array([[1, 1, 1, 1],
           [1, 1, 1, 1],
           [1, 1, 1, 1],
           [1, 1, 1, 1]])



### ndarray의 차원과 크기를 변경 : reshape()


```python
arr=np.arange(10)
print(arr.shape)
print(arr)
```

    (10,)
    [0 1 2 3 4 5 6 7 8 9]



```python
arr2=arr.reshape(2,5)
arr2
```




    array([[0, 1, 2, 3, 4],
           [5, 6, 7, 8, 9]])




```python
arr2=arr.reshape(3,3) # 리스트의 값과 정하는 행렬의 수가 맞아야 한다.
arr2
```


    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-38-3dc1b6036ad3> in <module>
    ----> 1 arr2=arr.reshape(3,3)
          2 arr2


    ValueError: cannot reshape array of size 10 into shape (3,3)


### 인덱싱: 특정 데이타 추출


```python
#------------------------------------------ (1) 단일값 출력
import numpy as np
arr = np.arange(1, 11)
print(arr)

## 세번째 요소 추출 ( 0부터 인덱스)
arr[3]


## 뒤에서 세번째 요소 추출 ( 뒤에서 인덱스는 -1부터)
arr[-3]

```

    [ 1  2  3  4  5  6  7  8  9 10]





    8




```python
## 1부터 9까지 nparray를 만들고 3행 3열 2차원 구조로 변경한후
## 두번째 행의 세번째 열의 값 추출
arr=np.arange(1,10)
arr2=arr.reshape(3,3)
print(arr2)
arr2[1][2]


```

    [[1 2 3]
     [4 5 6]
     [7 8 9]]





    6




```python
#------------------------------------------ (2) 슬라이싱 (:)
arr = np.arange(1, 10)

arr=arr.reshape(3,3)


```


```python
## 2차원 배열에서 생성
"""
    1 2 3
    4 5 6
    7 8 9
"""

    
## 행렬에서 1, 2, 4, 5 추출
arr[0]:[5]


## 행렬에서 4, 5, 6, 7, 8, 9 추출


## 행렬에서 2, 3, 5, 6 추출


## 행렬에서 1, 4 추출


## 행렬에서 전체 요소 추출


```


```python
# 2차원 ndarray에서 뒤의 오는 인덱스가 없으면 1차원으로 반환
# 3차원 ndarray에서 뒤의 오는 인덱스가 없으면 2차원으로 반환


```


```python
# 슬라이싱[:]과 인덱스선택을 결합

"""
    1 2 3
    4 5 6
    7 8 9
"""
import numpy as np
arr = np.arange(1, 10)
ndarr = arr.reshape(3,3)
print(ndarr)

## 행렬에서 1, 2, 4, 5 추출


## 행렬에서 4, 5, 6, 7, 8, 9 추출


## 행렬에서 2, 3, 5, 6 추출


## 행렬에서 1, 4 추출


## 행렬에서 3, 6 추출


# 지금은 너무 간단하다고 여기지만 추후에 데이타에서 많이 헷갈려서 여기서 시간 소요를 많이 한다
```


```python
#------------------------------------------ (3) 블린인덱싱
# 조건 필터링과 검색을 같이 하기에 자주 사용

arr = np.arange(1, 10)
ndarr = arr.reshape(3,3)
print(ndarr)

# 5보다 큰 요소들 추출


# 8값 요소를 88로 변경

```
