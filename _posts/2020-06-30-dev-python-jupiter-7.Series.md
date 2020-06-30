---
layout: post  
title: "[Python] Jupiter Notebook에서 Series"  
subtitle: "파이썬 Series 에 대한 기초적인 설명"  
categories: dev
tags: python
comments: true

---

> 파이썬 Series 에 대한 기초적인 설명



## Series

- DataFrame의 한 컬럼 데이터 세트

- Series 역시 DataFrame의 인덱스와 동일한 인덱스를 가진다

- 즉 Series는 컬럼이 하나인 데이타 구조체이고, DataFrame은 컬럼이 여러개인 데이타 구조체이다


> DataFrame을 RDBMS의 테이블과 유사하다면, Series는 테이블의 한 컬럼과 유사다하고 볼 수 있다



#### Series 의 사용

```python
# from pandas import Series # 이런식으로 한번에 Series만 import도 가능
import pandas as pd
age_in = pd.Series([22,33,44,25,28])
age_in
```




    0    22
    1    33
    2    44
    3    25
    4    28
    dtype: int64
<br/>

<br/>

#### 인덱스 값 가져오기

```python
age_in.index
```
	RangeIndex(start=0, stop=5, step=1) #인덱스 범위가 , 0부터 5'전'까지 있고 1씩 오른다.  

<br/>

<br/>

#### 값을 확인하기

```python
age_in.values #값만 볼때는 array타입으로 나오고 dtype은 int64 **단, 함수표시()를 하면 에러발생
```


    array([22, 33, 44, 25, 28], dtype=int64)

<br/>

<br/>

#### 키를 확인하기

```python
age_in.keys 
# keys는 인덱스의 별칭 == age_in.index 
# keys는 key, value / key, value로 값을 뽑음/ keys() 사용하면 인덱스를 부르는 것과 동일함
```


    RangeIndex(start=0, stop=5, step=1)



### 인덱스를 지정하며 시리즈를 생성하기

```python
age_in = pd.Series([22,33,44,25,28], index=['가','나','다','라','마'])
age_in
# 인덱스를 지정하지 않고 실행하면 0,1,2,3,..로 나오지만 인덱스를 지정하면 지정한 값이 나옴
```
    가    22
    나    33
    다    44
    라    25
    마    28
    dtype: int64

#### 인덱스를 지정한 경우 인덱스와 키,밸류를 조회 했을 때

```python
age_in.index # 인덱스
```


    Index(['가', '나', '다', '라', '마'], dtype='object')

<br/>


```python
age_in.keys #키
```


    <bound method Series.keys of 
    가    22
    나    33
    다    44
    라    25
    마    28
    dtype: int64>
<br/>

```python
age_in.values #값
```


    array([22, 33, 44, 25, 28], dtype=int64)

<br/>

<br/>

#### ''다'' 인덱스를 100으로 변경

```python
age_in['다'] = 100
age_in
```


    가     22
    나     33
    다    100
    라     25
    마     28
    dtype: int64
<br/>

<br/>

#### 중복된 시리즈 인덱스를 확인 하기

```python
# Series 인덱스 중복 확인
srs = pd.Series(['가','나','다'], index=['a','b','a'])
srs

print(srs['a']) # '가','다' 둘 다 출력
print(srs)
srs[0]   # 0번쨰 자리인 '가'만 출력
srs[-1]  # srs[2] 정방향 == srs[-1] 역방향 
```

    a    가
    a    다
    dtype: object
    a    가
    b    나
    a    다
    dtype: object
    
    '다'

<br/>

<br/>

### 딕셔너리를 시리즈 형태로 변환

```python
# 딕셔러리를 시리즈 형태로 변환
info_list = { 'kim': 25, 'park':22, 'lee':34 }

info_series = pd.Series(info_list) # 그냥 대입하는것으로 시리즈로 변경 가능
info_series
```


    kim     25
    park    22
    lee     34
    dtype: int64
<br/>

```python
# 'lee'의 점수를 90점으로 지정하기
info_series['lee'] = 90 # 결국 lee의 인덱스를 가진 행을 찾아 값을 90으로 변경하는 것이다.
info_series
```


    kim     25
    park    22
    lee     90
    dtype: int64
<br/>

#### 딕셔너리 시리즈 형태로 변환시 , 인덱스값을 따로 잡으면

```python
info_list = { 'kim': 25, 'park':22, 'lee':34 }

info_series = pd.Series(info_list, index=[0,1,2]) 
# 인덱스를 지정하면 원래 키로 가지고있던 kim,park,lee를 사용할 수 없고 그에 해당하는 값도 넣을 수 없다.
# 따라서 info_list를 가지고 시리즈를 만들겠다고 했지만 결국 0,1,2를 인덱스로 가지는 빈 시리즈를 만들게 되는것이다. 
# 인덱스도 넣고 싶고 원래 있는것도 살리고 싶을때, index=[0,1,2,'kim','park','lee'] 와 같이 코딩하면
# 원래 info_list가 가진 키밸류를 살리면서 새로운 0,1,2 인덱스를 생성할 수 있다.
info_series
```


    0       NaN
    1       NaN
    2       NaN
    dtype: float64


##  Series 인덱스

+ 리스트, 튜플의 index와  dict 의 key 와 유사

+ 같은 값의 index 가 가능 ( 즉, 중복 가능 ) 

-------------------------------------------------

<br/>
<br/>

## 정리

- 리스트 튜플 index : 일련번호로 변경불가 / 순서 개념이 있다

- Series Index : 중복 가능 / 순서 개념이 있다

- Dict key : 중복 불가 / 순서 개념 없다



## 판다스를 사용하는 이유


만일 파이썬의 리스트와 판다스의 Series가 거의 유사하다면, 우리는 왜 파이썬의 리스트가 아닌 판다스의 Series를 사용할까? 

파이썬의 리스트를 사용하면 판다스에서 제공하는 다양한 기능을 사용할 수 없기 때문이다.