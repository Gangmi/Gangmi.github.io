---
layout: post  
title: "[Python] Jupiter Notebook에서 Kenel"  
subtitle: "Kenel의 간단한 사용법"  
categories: dev
tags: python
comments: true
---

> 쥬피터 노트북에서 Kenel에 대한 간단한 사용법

## kernel : 현재 노트북의 실행하는 주체


```python
i=100
i*2
i   # [결과] 100 # ctl + enter 를 통해서 한 줄 실행이 가능하다 / 원하는 만큼 보고싶다면 print를 사용해야 한다.
```




    100




```python
import time

print('hello')
time.sleep(3) #작업을 하다보면 오래 걸리는데 이때 위의 정지 버튼을 누르면 끊긴다.
print('hi')
```

    hello
    hi



```python
print('hello')
time.sleep(10)
print('hi')
```

## 도중에 셀을 중단하려면? 

- 메뉴 > Kernel > Interrupt
- 메뉴 > Kernel > Restart

그러나 restart 후 다시 i값을 출력하려면 i 변수 없다고 에러발생

restart 후에는 각 셀들을 다시 실행해야 한다

아니면 메뉴 > Kernel > Restart & Run All


```python
i # kernel에서 restart만 누르고 i를 찾으라고 하면 찾지 못함 따라서 전체를 다시 시작하려면 restart-runall 해야함
    #또는 cell에서 현재 셀을 기준으로 어디까지 실행할건지 지정하는것이 보통이다.
```


    ---------------------------------------------------------------------------
    
    NameError                                 Traceback (most recent call last)
    
    <ipython-input-1-397d543883c5> in <module>
    ----> 1 i


    NameError: name 'i' is not defined

