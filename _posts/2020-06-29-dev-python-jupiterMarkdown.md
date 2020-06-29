---
layout: post  
title: "[Python] Jupiter Notebook 마크다운 사용"  
subtitle: "쥬피터 노트북에서 마크다운 문법사용"  
categories: dev
tags: python
comments: true
---

> 쥬피터 노트북에서 마크다운 문법을 사용하는 대략적인 방법

```python
# b를 누르면 현재행 아래로 행이 만들어지고 a를 누르면 위로 만들어진다.
```


```python
# m을 누르면 마크다운으로  y를 누르면 실행모드
```


```python
# 줄을 삭제 하려면 dd를 하면됨
```


```python
# 줄을 삭제 하려면 dd를 하면됨
```

#### 쉘모드 변경
+ Code 쉘 : esc > y
+ markdown 쉘 : esc > m

##### 마크다운 쉘에서 문서 만들기

#서울 지하철 평균 이용객 수 분석

### 가장 이용객이 많은 지하철은?

+ 강남
+ 홍대

    - 성수
    - 합정

* 별표 하나는 번호 없는 목록

*별표로 감싸면 기울이기 (주의:* 와 글자사이에 공백 안 됨)* 

-> 별표가 붙은 양옆 문자를 말함

**별표 두개는 굵게**

***별표 3개는 굵게 기울이기***

가로선 ---

---


> 인용문이지만 많이 사용

<div align='center'> 헬로우 월드 </div>


[링크걸기](http://www.data.go.kr)

이미지링크

글씨가 아니라고 지정해야함
                          
                          
[![텍스트](https://t1.daumcdn.net/daumtop_chanel/op/20170315064553027.png)](https://www.daum.net) 




## <font color='green'>코드결과</font>


```python
import pandas

p1=pandas.read_csv('dataset/subway_data1.csv',encoding='utf-8')
p1
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
      <th>구 분</th>
      <th>역명</th>
      <th>총계</th>
      <th>일평균</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1호선</td>
      <td>서울역</td>
      <td>11,933,924</td>
      <td>132,599</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1호선</td>
      <td>시청역</td>
      <td>4,221,693</td>
      <td>46,908</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1호선</td>
      <td>종각역</td>
      <td>8,441,749</td>
      <td>93,797</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1호선</td>
      <td>종로3가역</td>
      <td>6,725,558</td>
      <td>74,728</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1호선</td>
      <td>종로5가역</td>
      <td>5,038,305</td>
      <td>55,981</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>90</th>
      <td>4호선</td>
      <td>이촌역</td>
      <td>1,792,511</td>
      <td>19,917</td>
    </tr>
    <tr>
      <th>91</th>
      <td>4호선</td>
      <td>동작역</td>
      <td>523,615</td>
      <td>5,818</td>
    </tr>
    <tr>
      <th>92</th>
      <td>4호선</td>
      <td>총신대입구역</td>
      <td>4,398,897</td>
      <td>48,877</td>
    </tr>
    <tr>
      <th>93</th>
      <td>4호선</td>
      <td>사당역</td>
      <td>5,459,335</td>
      <td>60,659</td>
    </tr>
    <tr>
      <th>94</th>
      <td>4호선</td>
      <td>남태령역</td>
      <td>206,457</td>
      <td>2,294</td>
    </tr>
  </tbody>
</table>
<p>95 rows × 4 columns</p>
</div>



<table>
    <tr><td>인덱스</td><td>값</td></tr>
    <tr><td>1</td><td>1호선</td></tr>
</table>


```python
#이미지에 링크 걸기
#[![원하는텍스트](이미지경로)](연결할링크주소)
```

[연습]

지하철이미지 출력

그이미지 클릭하면 지하철 홈페이지로 연결



[![ㅜㅜ](/assets/img/dev/python/linux-logo.png)](https://www.daum.net) 



