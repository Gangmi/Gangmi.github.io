---
layout: post  
title: "[Python] Jupiter Notebook을 이용한 데이터 분석"  
subtitle: "파이썬의 데이터 분석 패키지를 통한 데이터 분석 및 시각화"  
categories: dev
tags: python
comments: true
---

> 파이썬 데이터 분석 패키지들에대한 소개 및 파이썬 공부방법

<br/>
<br/>
# 파이썬 데이터 분석 주요 패키지 

<br/>
<br/>



###  1. Numpy

- 행렬 / 선형대수 / 통계 패키지

- 머신러닝의 이론적 백그라운드는 선형대수와 통계로 이루어져 있다

- 사이킷런 같은 머신러닝 패키지가 넘파이 기반으로 되어 있다

    [데이타사이언스](https://datascienceschool.net/view-notebook/35099ac4aea146c69cc4b3f50aec736f/)

    [공식페이지](https://scipy.org/)

### 2. Scipy

- 자연과학과 통계를 위한 다양한 패키기

- 머신러닝 패키지인 사이킷런에서도 Scipy 패키지로 구축된 여러가지 패키지를 제공한다

    [공식페이지](https://scipy.org/)

### 3. Pandas

- 대표적인 데이터 처리 패키지
- 판다스는 2차원 데이터 처리에 특화되어 있다
  ( 넘파이가 행렬기반의 데이타를 처리에 특화되어 있어서 일반 데이타 처리가 부족한데 반해)
- matplotlib을 호출하여 쉽게 시각화하는 구조

    [참고페이지](http://pandas.pydata.org/pandas-docs/stable/reference/index.html)

### 4. Matplotlib / Seaborn

- 파이썬의 대표적인 시각화 패키지
- 시각적인 디자인 부분이 투박하고 단순한 시각화 표현에도 코드가 길어질 수 있다
- matplotlib를 보완하기 위한 패키지가 seaborn 이다

    [matplotlib 참고](https://matplotlib.org/)
    
    [seaborn 참고](https://seaborn.pydata.org/)

## 라이브러리 설치

+ Anaconda prompt를 관리자 권한으로 실행
> pip install 라이브러리명

---
---

### 도움말

?변수 또는 변수?  >  shift + enter

?함수             >  shift + enter

또는 변수나 함수에 커서 놓고 > shift + tab

*타이핑 하면서 탭키를 누르면 완성된다*

[ 참고 ] [데이타사이언트스쿨](https://datascienceschool.net/view-notebook/5a3b9aaade8545c38ab4b888dd9516d4/)

## 크롬으로 변경하려면

먼저 크롬을 열고 서버 콘솔 창에 있는 주소르 복사하여 URL 경로에 붙인다

ex) http://localhost:8888/?token=cd1933550bfed6c793c10636004dd6fa50306e2e66ab51c8

---

### % 매직명령어

%ls : 현재 디렉토리의 목록

%pwd : 현재 작업 경로

%history : 입력했던 명령어 내역

%matplotlib inline : 기본이 새창으로 그래프를 출력하는데, 그래프의 결과를 출력차에 그래도 표현되도록



### ! OS 명령

!dir/w

!ls

!conda list


### 쉘모드 변경
+ Code 쉘로 변경 : esc > y
+ Markdown 쉘로 변경 : esc > m


```python

```

---
---

## * [ 공부하는 방식 ]

기존 자바는 A -> B - > C 순으로 A를 익히고 B를 공부한다.
그러나 파이썬 저자나 전문가들이 추천하는 공부 방법은 A -> B -> C - > D를 가볍게 공부하고
C에서 다시 A가 필요하면 그 때 다시 A를 공부하고
D에서 다시 A와 B가 필요하면 다시 A와 B를 공부하는 방식으로 하는 것이 좋다고 한다.

물론 A를 마스터(?)하고 B를 넘어가고자 할 수 있지만
이런 식으로 공부하면 더디고 지쳐서 중도포기할 수 있기 때문이다.


#### 즉 파이썬은 기초를 완벽하게 다지고 단계 단계를 거치는 것보다
#### 예제를 풀 때 부딪치며 모르는 부분을 API나 인터넷을 찾으면서 공부하는 것을 권장한다

넘파이와 판다스에 대한 기본 사항을 습득하고 일단 코드와 부딪쳐 가면서 모르는 API에 대해서는 찾아가며 습득하는 것이 머신러닝 뿐만 아니라 넘파이, 판다스에 관한 이해를 넓히는 빠른 방법이다

그래서 우리는 기본 사항을 잘 정리해야 한다.
다시 이해해야 할 상황에 다시 익히고 추가할 내용을 다시 추가하여 정리하는 방식으로 파이썬을 완성해 나아가 한다.
