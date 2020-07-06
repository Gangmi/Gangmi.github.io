---
layout: post  
title: "[Python] Jupiter Notebook에서 apply"  
subtitle: "파이썬 apply 에 대한 기초적인 설명"  
categories: dev
tags: python
comments: true

---

> 파이썬 apply에 대한 기초적인 설명

## apply
- 행 또는 열 또는 전체의 셀에 원하는 연산을 지원한다.
- 단일 연산의 경우 전체에 적용된다.
- 원하는 함수를 원하는 곳에 넣어 사용하는것이 가능하다.


#### 사용할 DataFrame을 생성
```python
import pandas as pd

df = pd.DataFrame( {'a':[10,20,30], 'b':[2, 4, 6]})
df
```
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



#### apply로 사용할 함수 정의
```python
# 1. 함수 정의
def my_fun1(x):
    return x**2 # 자승을 하는 함수
 
def my_fun2(x, n): # 자승을 몇번할지를 계산하는 함수
    return x**n

print(my_fun1(4)) # 4의 2승
print(my_fun2(4,3)) #4의 3승 
```
    16
    64
#### 일반적으로 함수에 DataFrame을 대입하는것과 apply의 비교
```python
# 2. apply 함수를 이용하여 모든 데이타에 각각 함수 적용하기

print(my_fun1(df['a'])) #my_fun1함수에 df 의 a 컬럼을 대입
print('-'*50)

print(my_fun1(df)) # 해당 함수에 df 를 통으로 넣음
print('-'*50)
      
#위의것과 동일하게 결과를 도출하지만 가독성을 위해 사용한다.
#해당 요소를 어느 함수에 넣는지를 표시

print(df['a'].apply(my_fun1))
print('-'*50)
print(df['a'].apply(my_fun2,n=3)) #인자를 2개 받는 함수이기 때문에 따로 인자를 줘야한다.
print('-'*50)

df['a'].apply(lambda x: my_fun1(x)) #람다 형식으로 넣는것도 가능하다.
```
 	#my_fun1함수에 df 의 a 컬럼을 대입
    0    100
    1    400
    2    900
    Name: a, dtype: int64
    --------------------------------------------------
    # 해당 함수에 df 를 통으로 넣음
         a   b
    0  100   4
    1  400  16
    2  900  36
    --------------------------------------------------
    my_fun1함수에 df 의 a 컬럼을 대입 (apply사용)
    0    100
    1    400
    2    900
    Name: a, dtype: int64
    --------------------------------------------------
    #my_fun2 에 apply를 사용해서 값을 대입 n=3
    0     1000
    1     8000
    2    27000
    Name: a, dtype: int64
    --------------------------------------------------
    #my_fuc1을 람다를 통해 대입한 결과
    0    100
    1    400
    2    900
    Name: a, dtype: int64




```python
# [연습] 데이타 프레임의 각 열 단위로 데이타의 합을 출력
def my_fun3(col):
    sum=0
    for i in col:
        sum += i
    return sum
print(df)
print('-'*50)
#my_fun3에 df의 a 컬럼 대입
print(my_fun3(df['a']))
print('-'*50)

#df의 a컬럼을 apply를 통해 대입
print(df.apply(my_fun3)) #열단위로
print('-'*50)
print(df.apply(my_fun3, axis=1)) #행단위로
```

        a  b
    0  10  2
    1  20  4
    2  30  6
    --------------------------------------------------
    60
    --------------------------------------------------
    a    60
    b    12
    dtype: int64
    --------------------------------------------------
    0    12
    1    24
    2    36
    dtype: int64



```python
# 'a' 컬럼의 값이 10 이하는 'C', 20 이하는  'B', 30 이하는 'A'를 지정하고자 할 때
def func(score):
    grade = ''
    if( score <= 10) : grade='C'
    elif(score <= 20) : grade='B'
    elif(score <= 30) : grade='A'
    return grade

#df를 apply로 대입
#df['a'].apply(  func() # 여기서 이 괄호가 들어가면 안 된다.  )
print(df)
print(df['a'].apply(func))
```

        a  b
    0  10  2
    1  20  4
    2  30  6
    0    C
    1    B
    2    A
    Name: a, dtype: object


## [연습]  고객의 결제정보에서 vip 선별

결재가 confirmed 된 상태이고 금액이 500원이상 구매한 고객들을 vip로 선별하고 그 외 고객들은 non-vip로 지정하여 grade 컬럼에 추가 저장한다.


```python
import pandas as pd

# index_col : 지정한 컬럼을 Row Index로 사용한다.
customer = pd.read_csv('./data/customer.csv', index_col = "Name")


```


```python


#1) 결재가 confirmed 된 상태이고 금액이 500원 이상에 대한 조건 값을 먼저 넣는다.(true/false)
customer['grade']= (customer['state']=='confirmed') & (customer['price']>=500)
print(customer)


#2) 함수 선언(true 이면 vip지정하고, false이면 non-vip)
def vip(col):
    grade = ''
    if( col == True) : grade='vip'
    elif(col== False) : grade='non-vip'
    
    return grade


#3) grade 컬럼과 2번의함수와 연결(apply)사용 가능 
customer['grade']=customer['grade'].apply(vip) # 리턴을 다시 해당 컬럼으로 받아줘야 들어감
print(customer)

#customer['grade']=customer['grade'].apply(lambda x:vip(x))
#print(customer)

#람다로도 가능하다


```

                date  price      state  grade
    Name                                     
    Kang  2017-01-01    500  confirmed   True
    Kim   2017-01-03    700  confirmed   True
    Choi  2017-01-03    900  confirmed   True
    Park  2017-01-05    800  confirmed   True
    Lee   2017-01-07    500   canceled  False
    Yoon  2017-01-09    700  confirmed   True
    Jang  2017-01-09    600   canceled  False
    Ko    2017-01-10    200   canceled  False
                date  price      state    grade
    Name                                       
    Kang  2017-01-01    500  confirmed      vip
    Kim   2017-01-03    700  confirmed      vip
    Choi  2017-01-03    900  confirmed      vip
    Park  2017-01-05    800  confirmed      vip
    Lee   2017-01-07    500   canceled  non-vip
    Yoon  2017-01-09    700  confirmed      vip
    Jang  2017-01-09    600   canceled  non-vip
    Ko    2017-01-10    200   canceled  non-vip


