---
layout: post  
title: "[Python] Jupiter Notebook에서 DataFrame의 개념"  
subtitle: "Data Frame 의 개념"  
categories: dev
tags: python
comments: true
---

> 쥬피터 노트북에서 파이썬의 Pandas를 사용하기 위해 알고있어야할 DataFrame개념

<br/>
<br/>

# 판다스(Pandas)
> 파이썬에서 사용하는 데이터 분석 라이브러리 중의 하나로, 행과 열로 이루어진 데이터 객체를 
> 만들어 다룰수 있다. 또한 보다 안정적으로 대용량의 데이터들을 처리하는데 매우 편리한 도구다.

- 판다스의 핵심 객체는 DataFrame이다. 
- 데이터 프레임은 2차원 데이터 구조체로 numpy보다 편리하게 데이터를 핸들링한다.
- R 언어의 데이터 프레임과 비슷하고 많이 사용된다.
<br/>
<br/>

#### Data Frame에서 데이터 필터링 (추출하기)

```python
# 먼저 데이터 프레임 자료를 생성 하고 해당 데이터를 pandas로 담는다.
import pandas as pd # 판다스를 import 한다.

mydata = {
          'name':['홍길동','박길동','김길동'], 
          'age':[22,33,44], 
          'dept':['컴공','국어','산업']
         }

df = pd.DataFrame(mydata) #테이블구조로 출력됨
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>22</td>
      <td>컴공</td>
    </tr>
    <tr>
      <th>1</th>
      <td>박길동</td>
      <td>33</td>
      <td>국어</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44</td>
      <td>산업</td>
    </tr>
  </tbody>
</table>
</div>

#### 기본적인 사용법

1. 열(컬럼) 추출
	+ df.컬럼명
	+ df.['컬럼명']

2. 행 추출
	+ df.loc[ ] : 인덱스(순서)와 명칭으로 추출
	+ df.iloc[ ] : 인덱스(순서)로 추출
	+ df.ix[ ] : 명칭 기반 인덱싱과 위치 기반 인덱싱 모두 사용 (* 그러나 곧 사라질 예정)

> 위의 행추출관련 3개의 연산자는 노련한 개발자들도 혼동하기에 , 일반적으로 하나만 선택해서
> 사용하는것을 권장한다. 넘파이와 유사한 부분으로 더욱 혼동하기 쉽다.

3. 행과 열에서 추출
	+ df.loc[2,3] : 2 행의 3열 데이터
	+ df.loc[1:3, 2:4] : 1부터 2행(3-1)까지의 행에서 2~3(4-1) 열의 데이터 ?????????????????


#### 예제

##### 열 추출 : 이름만 추출
```python
print(df.name)
print(df['name'])
```

    0    홍길동
    1    박길동
    2    김길동
    Name: name, dtype: object
<br/>

##### 2번 행을 추출   
```python
print(df.loc[2]) # 순서로 0부터 1,2
print(df.iloc[2]) #인덱스로 
```
 name    김길동
    age      44
    dept     산업
    Name: 2, dtype: object
    
 name    김길동
    age      44
    dept     산업
    Name: 2, dtype: object
    
<br/>
##### 값 추출 예제
```python
# 값만 추출
print(df.values)
print('-'*50)

# 컬럼명 추출
print(df.columns)
print('-'*50)

# 인덱스만 추출
print(df.index)
print(df.keys()) # 컬럼명 추출
```
[['홍길동' 22 '컴공']
     ['박길동' 33 '국어']
     ['김길동' 44 '산업']]
    --------------------------------------------------
    Index(['name', 'age', 'dept'], dtype='object')
    --------------------------------------------------
    RangeIndex(start=0, stop=3, step=1)
    Index(['name', 'age', 'dept'], dtype='object')

##### 인덱스 지정하기

```python
df2 = pd.DataFrame(mydata, index=['일','이','삼'])
df2
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>일</th>
      <td>홍길동</td>
      <td>22</td>
      <td>컴공</td>
    </tr>
    <tr>
      <th>이</th>
      <td>박길동</td>
      <td>33</td>
      <td>국어</td>
    </tr>
    <tr>
      <th>삼</th>
      <td>김길동</td>
      <td>44</td>
      <td>산업</td>
    </tr>
  </tbody>
</table>
</div>

<br/>

##### 박길동을 추출
```python
# '박길동'을 추출
df2.loc['이']['name'] # 인덱스와 명칭으로 추출
```

    '박길동'
<br/>
<br/>
##### 컬럼 추가, 행 추가

```python
# 컬럼 추가
df['gender'] = ['여','남','여'] # 원래 없었던 컬럼을 만들면서 바로 값을 넣음
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>22</td>
      <td>컴공</td>
      <td>여</td>
    </tr>
    <tr>
      <th>1</th>
      <td>박길동</td>
      <td>33</td>
      <td>국어</td>
      <td>남</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44</td>
      <td>산업</td>
      <td>여</td>
    </tr>
  </tbody>
</table>
</div>

<br/>
<br/>

##### 행 추가
```python
df.loc[3] = ['박길동',33, '컴', '남']
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>22</td>
      <td>컴공</td>
      <td>여</td>
    </tr>
    <tr>
      <th>1</th>
      <td>박길동</td>
      <td>33</td>
      <td>국어</td>
      <td>남</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44</td>
      <td>산업</td>
      <td>여</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박길동</td>
      <td>33</td>
      <td>컴</td>
      <td>남</td>
    </tr>
  </tbody>
</table>
</div>

<br/>
<br/>
##### 행추가 +1

```python
df.loc[9] = ['고길동',33, '컴', '남']
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>22</td>
      <td>컴공</td>
      <td>여</td>
    </tr>
    <tr>
      <th>1</th>
      <td>박길동</td>
      <td>33</td>
      <td>국어</td>
      <td>남</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44</td>
      <td>산업</td>
      <td>여</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박길동</td>
      <td>33</td>
      <td>컴</td>
      <td>남</td>
    </tr>
    <tr>
      <th>9</th>
      <td>고길동</td>
      <td>33</td>
      <td>컴</td>
      <td>남</td>
    </tr>
  </tbody>
</table>
</div>
<br/>
<br/>
##### 인덱스 변경

```python
# 인덱스순서를 변경하려면 -> 인덱스는 우선 DataFrame이 있는 상태에서 변경해야 한다
df = df.reindex(index=[0,2,5,3,1])  # 인덱스 5번의 값이 없으므로 nan이 나온다.

# 변경전, 0의 인덱스를 가진것을 0번째로 2의 인덱스를 가진것을 1번째로 ......1의 
#인덱스를 가진 것을 4번째로 하겠다는 것이다. 

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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>22.0</td>
      <td>컴공</td>
      <td>여</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44.0</td>
      <td>산업</td>
      <td>여</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>컴</td>
      <td>남</td>
    </tr>
    <tr>
      <th>1</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>국어</td>
      <td>남</td>
    </tr>
  </tbody>
</table>
</div>

##### 값의 변경 및 계산

```python
# 컬럼연산
df['age+10'] = df['age']+10
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
      <th>gender</th>
      <th>age+10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>22.0</td>
      <td>컴공</td>
      <td>여</td>
      <td>32.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44.0</td>
      <td>산업</td>
      <td>여</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>컴</td>
      <td>남</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>국어</td>
      <td>남</td>
      <td>43.0</td>
    </tr>
  </tbody>
</table>
</div>

> 이런식으로 만약 해당하는 컬럼이 없다면 새로 만들고 값을 넣는다.


```python
# 5 행에 'dept'열의 값을 '인문'으로 변경
# df['dept'][5]='인문' # dept컬럼의 5번인덱스를 가진 셀을바꿈
df.loc[5,'dept'] = '인문'
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
      <th>gender</th>
      <th>age+10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>22.0</td>
      <td>컴공</td>
      <td>여</td>
      <td>32.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44.0</td>
      <td>산업</td>
      <td>여</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>인문</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>컴</td>
      <td>남</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>국어</td>
      <td>남</td>
      <td>43.0</td>
    </tr>
  </tbody>
</table>
</div>

<br/>
<br/>

###  컬럼 속성 추출

```python
# 컬럼 속성 추출 (성별 추출)
df.gender
df['gender']
```


    0      여
    2      여
    5    NaN
    3      남
    1      남
    Name: gender, dtype: object


<br/>
<br/>
```python
# 특정 컬럼의 특정행 추출 -> 즉 특정셀 추출 
df.loc[2,'dept'] #2번 인덱스의 dept 컬럼값은?
df.loc[2]['dept']
df.loc[2].dept

df['dept'][2] #dept 컬럼의 2번 인덱스는?
df.dept[2]
```

    '산업'
<br/>
<br/>
```python
# 30세 이상의 레코드 겁색
# df['age']>=30 #bool -> True, False로 추출

df[df['age']>=30] # 이런식으로 조건식이 안쪽에 들어가는 것도 가능하다.
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
      <th>gender</th>
      <th>age+10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44.0</td>
      <td>산업</td>
      <td>여</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>컴</td>
      <td>남</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>국어</td>
      <td>남</td>
      <td>43.0</td>
    </tr>
  </tbody>
</table>
</div>
<br/>
<br/>

##### 인덱스 1의 값을 '맹길동' 으로 변경하려면?
```python
df.loc[1,'name']='맹길동'
df
df[1,'name']='최길동'#실수로 loc을 뺴고 입력을 했을 시 컬럼으로 간주되어 추가됨
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
      <th>gender</th>
      <th>age+10</th>
      <th>(1, name)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>22.0</td>
      <td>컴공</td>
      <td>여</td>
      <td>32.0</td>
      <td>최길동</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44.0</td>
      <td>산업</td>
      <td>여</td>
      <td>54.0</td>
      <td>최길동</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>인문</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>최길동</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>컴</td>
      <td>남</td>
      <td>43.0</td>
      <td>최길동</td>
    </tr>
    <tr>
      <th>1</th>
      <td>맹길동</td>
      <td>33.0</td>
      <td>국어</td>
      <td>남</td>
      <td>43.0</td>
      <td>최길동</td>
    </tr>
  </tbody>
</table>
</div>
<br/>
<br/>
### 데이터 필터링

- 넘파이와 유사한 부분으로 더욱 혼동하기 쉽다.

- 판다스의 DataFrame과 Series에서도 다른 부분이 있어서 주의해야 한다.

```python
print(df.loc[1]) # 인덱스를 명칭으로 취급하여 출력
print('-'*50)
print(df.iloc[1]) # 순수 인덱스로 취급하여 0번째~... 순서로 출력 
```

    name         맹길동
    age           33
    dept          국어
    gender         남
    age+10        43
    (1, name)    최길동
    Name: 1, dtype: object
    --------------------------------------------------
    name         김길동
    age           44
    dept          산업
    gender         여
    age+10        54
    (1, name)    최길동
    Name: 2, dtype: object

```python
print(df.loc[1,'dept']) #순서를 따지는 것이 아니라 이름으로 따짐(이름을 줘야함)
print('-'*50)
print(df.iloc[1,2]) #1행 2열 값 추출 (인덱스 순번에 따라 값 추출(x,y는 x행 / y열에 해당하는 값))
```

    국어
    --------------------------------------------------
    산업

##### loc 와 iloc 의 차이점

```python
# 명칭기반 인덱스 : 문자열이 인덱스인 경우
df2 = pd.DataFrame(mydata, index=['일','이','삼']) 
df2.loc['이'] #명칭, 순번 둘 다 처리 가능
df2.iloc[1] #순번으로 처리하기 때문에 숫자를 써야함 
```
    name    박길동
    age      33
    dept     국어
    Name: 이, dtype: object

##### 특정 컬럼으로 인덱스를 지정하는것도 가능하다.

```python
# 특정 컬럼으로 인덱스를 지정 inplace=True 지정 시 name이 인덱스가 됨
df2.set_index('name', inplace=True)
df2
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
      <th>age</th>
      <th>dept</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>홍길동</th>
      <td>22</td>
      <td>컴공</td>
    </tr>
    <tr>
      <th>박길동</th>
      <td>33</td>
      <td>국어</td>
    </tr>
    <tr>
      <th>김길동</th>
      <td>44</td>
      <td>산업</td>
    </tr>
  </tbody>
</table>
</div>

#### 정렬과 T
```python
# 나이를 오름차순으로 ( sort_values() )
# df.sort_index(ascending=0)   # 인덱스 정렬 기본값이 ascending=1
# df

# 두 개다 같은 코딩이지만 위의 코딩은 원분이 변경되지 않고 밑의 코딩은 원본이 변경됨
df = df.sort_values('age') 
df.sort_values('age', inplace=True, ascending=False) # 나이를 내림차순으로
df
# 전문가들은 원본이 변경되지 않는 것을 권장 
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
      <th>name</th>
      <th>age</th>
      <th>dept</th>
      <th>gender</th>
      <th>age+10</th>
      <th>(1, name)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>김길동</td>
      <td>44.0</td>
      <td>산업</td>
      <td>여</td>
      <td>54.0</td>
      <td>최길동</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박길동</td>
      <td>33.0</td>
      <td>컴</td>
      <td>남</td>
      <td>43.0</td>
      <td>최길동</td>
    </tr>
    <tr>
      <th>1</th>
      <td>맹길동</td>
      <td>33.0</td>
      <td>국어</td>
      <td>남</td>
      <td>43.0</td>
      <td>최길동</td>
    </tr>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>22.0</td>
      <td>컴공</td>
      <td>여</td>
      <td>32.0</td>
      <td>최길동</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>인문</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>최길동</td>
    </tr>
  </tbody>
</table>
</div>
<br/>
<br/>

##### 행과 열 바꾸기

```python
df.T # T : 행과열을 바꿔줌
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
      <th>2</th>
      <th>3</th>
      <th>1</th>
      <th>0</th>
      <th>5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>name</th>
      <td>김길동</td>
      <td>박길동</td>
      <td>맹길동</td>
      <td>홍길동</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>age</th>
      <td>44</td>
      <td>33</td>
      <td>33</td>
      <td>22</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>dept</th>
      <td>산업</td>
      <td>컴</td>
      <td>국어</td>
      <td>컴공</td>
      <td>인문</td>
    </tr>
    <tr>
      <th>gender</th>
      <td>여</td>
      <td>남</td>
      <td>남</td>
      <td>여</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>age+10</th>
      <td>54</td>
      <td>43</td>
      <td>43</td>
      <td>32</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>(1, name)</th>
      <td>최길동</td>
      <td>최길동</td>
      <td>최길동</td>
      <td>최길동</td>
      <td>최길동</td>
    </tr>
  </tbody>
</table>
</div>
<br/>
<br/>
### 정보확인

```python
# 총 데이터 건수와 데이타 타입등 정보 확인
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 5 entries, 2 to 5
    Data columns (total 6 columns):
     #   Column     Non-Null Count  Dtype  
    ---  ------     --------------  -----  
     0   name       4 non-null      object 
     1   age        4 non-null      float64
     2   dept       5 non-null      object 
     3   gender     4 non-null      object 
     4   age+10     4 non-null      float64
     5   (1, name)  5 non-null      object 
    dtypes: float64(2), object(4)
    memory usage: 440.0+ bytes

### 기본 통계 구하기
```python
# 기본통계량 구하기 ( 총개수, 평균, 표준편차, 최소값, 4분위수 등)
df.describe()
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
      <th>age</th>
      <th>age+10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4.000000</td>
      <td>4.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>33.000000</td>
      <td>43.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>8.981462</td>
      <td>8.981462</td>
    </tr>
    <tr>
      <th>min</th>
      <td>22.000000</td>
      <td>32.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>30.250000</td>
      <td>40.250000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>33.000000</td>
      <td>43.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>35.750000</td>
      <td>45.750000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>44.000000</td>
      <td>54.000000</td>
    </tr>
  </tbody>
</table>
</div>






