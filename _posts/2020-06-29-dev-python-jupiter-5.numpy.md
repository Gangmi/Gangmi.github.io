---
layout: post  
title: "[Python] Jupiter Notebook에서 numpy"  
subtitle: "쥬피터 노트북에서 파이썬의 numpy의 사용"  
categories: dev
tags: python
comments: true
---

> 쥬피터 노트북에서 파이썬의 numpy의 사용

<br/>
<br/>
# numpy

>numpy란 , C 언어로 구현된 파이썬 라이브러리로 고성능의 수치 계산을 위해 제장 되었다.
>Numerical Python의 줄임말로 numpy는 벡터 및 행렬 연산에 있어서 매우 편리한 기능들을 제공한다.

<br/>
- 행렬 / 선형대수 / 통계 패키지
- 머신러닝의 이론적 백그라운드는 선형대수와 통계로 이루어져 있다
- 사이킷런 같은 머신러닝 패키지가 넘파이 기반으로 되어 있다
- 데이터 분석시 사용되는 라이브러리인 pandas와 matplotlib의 기반으로 사용되기도 한다.




    * 머신러닝 알고리즘이나 사이파이와 같은 과학, 통계 지원용 패키지를 직접 만드는 개발이 아니라면
    넘파이를 상세하기 알 필요는 없다지만, 넘파이를 이해하는 것이 파이썬 기반의 데이타분석과 머신러닝에 중요하다
    
    * 넘파이가 데이타 핸들링에 효율적으로 쉽고 편하고 할 수 없다.
      그러나 데이타 핸들링에 주로 사용하는 판다스도 많은 부분이 넘파이를 기반으로 만들어져 있다.
    
    * ndarray 
        - 넘파이 기반 데이타 타입
        - np.array()

<br/>
<br/>

> 이해를 돕기위한 코딩 예제

### numpy 형 만들기

```python
import numpy as np # numpy를 사용하기위해서 필요하다

#리스트 2개를 선언한다.

list_1=[1,2,3]
list_2=[9,8,7]

#리스트 2개를 모두 넘파이 array로 대입한다.
arr =np.array([list_1,list_2]) 

print(arr) # 리스트 2개가 arr에 저장되어있는것을 볼 수 있다.

```
    [[1 2 3]
     [9 8 7]]
<br/>
<br/>
### 해당 array의 모양을 알려주는 요소
```python
arr.shape # 몇행 몇 열인지를 알려주는 것
```
    (2, 3)

<br/>
<br/>
### array의 요소를 지정
```python

#두번째 행 두번째 열의 요소를 100으로 지정

arr[1][1]=100
arr
```
    array([[  1,   2,   3],
           [  9, 100,   7]])

<br/>
<br/>
### 도움말 부르기

```python
?arr # 도움말 부르기
```
<br/>
<br/>
### numpy array 여러 요소
```python
arr1=np.array([1,2,3]) # 이렇게 바로 선언하는것도 가능하다.
arr2=np.array([[1,2,3]])

print(arr1.shape) # (3,)
print(arr2.shape)

print(arr1.ndim,"차원")
print(arr2.ndim,"차원")
```
    (3,) #3개의 요소를 가지고 있는 튜플 이라는뜻 1차원에서는 이런식으로 표현
    (1, 3) #2차원부터 1행 3열이라고 표시
    1 차원
    2 차원

<br/>
<br/>
### numpy array의 자료형

```python
print(arr.dtype)
```
    int32

<br/>
### numpy array 값의 data type 을 변경
```python
arr2=arr.astype(np.float64) # 실수형 사용할 때 뒤에 0붙는것을 생략하고 .만 씀
arr2
```

    array([[  1.,   2.,   3.],
           [  9., 100.,   7.]])
           
<br/>
### numpy array의 자료형
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
<br/>

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
a2=np.zeros((5,5),dtype='int32') # 0으로 된 배열을 생성
a2
```

    array([[0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0]])


```python
a3=np.ones((4,4),dtype='int32') #1로된 배열을 생성
a3
```

    array([[1, 1, 1, 1],
           [1, 1, 1, 1],
           [1, 1, 1, 1],
           [1, 1, 1, 1]])



### ndarray의 차원과 크기를 변경 : reshape()


```python
arr=np.arange(10) # 0부터 9까지 값을 넣음
print(arr.shape)
print(arr)
```

    (10,)
    [0 1 2 3 4 5 6 7 8 9]



```python
arr2=arr.reshape(2,5) # 2차원배열 2행 5열로 변경
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

<br/>
<br/>

### 인덱싱: 특정 데이타 추출 예제


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

arr=arr.reshape(3,3) # 3행 3열로 변환


```


```python
## 2차원 배열 생성
"""
    1 2 3
    4 5 6
    7 8 9
"""
    
## 행렬에서 1, 2, 4, 5 추출
print(arr[:2,:2]) # 0부터 1까지행의, 0부터 1까지 열의 값을 가져옴


## 행렬에서 4, 5, 6, 7, 8, 9 추출
print(arr[1:3,0:]) #1행부터 2행까지 0부터 끝까지 값을 가져옴

## 행렬에서 2, 3, 5, 6 추출
print(arr[:2,1:3])

## 행렬에서 1, 4 추출
print(arr[:2,:1])

## 행렬에서 전체 요소 추출
print(arr1[:3,:3])

```
<br/>
<br/>
### 값을 추출할 때
```python
# 2차원 ndarray에서 뒤의 오는 인덱스가 없으면 1차원으로 반환
# 3차원 ndarray에서 뒤의 오는 인덱스가 없으면 2차원으로 반환
```
<br/>
<br/>

### 불린 인덱싱
```python
#------------------------------------------ (3) 블린인덱싱
# 조건 필터링과 검색을 같이 하기에 자주 사용

arr = np.arange(1, 10)
ndarr = arr.reshape(3,3)
print(ndarr)

# 5보다 큰 요소들 추출
print(ndarr>5) 
#이렇게 하면 
#[False False False False False  True  True  True  True]
#가 나오게 된다.
#따라서 ndarr[] 안에 이 조건식을 사용하면 ,
print(ndarr[ndarr>5])
[6 7 8 9] #이렇게 원하는 값을 가져올 수 있다.

# 8값 요소를 88로 변경
ndarr[2][1]=88

```
