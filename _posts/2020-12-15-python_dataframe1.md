---
layout: post
title: "[python] 그룹별 수치 상위 N개 추출/결측치 아닌 행만 추출/문자열에서 숫자만 추출"
excerpt: "데이터프레임에서 특정함수를 사용해 필요한 데이터를 불러보자."
author: Dayeon Lee
date: 2020-12-15 23:00:00 +0800
tags: [python, groupby, sort_values, notnull, isnull, re]
---

## 1. 그룹별 수치 상위 N개 불러오기
### groupby함수와 apply함수 이용하기 

> groupby : 데이터프레임에서 특정 열을 기준으로 데이터를 묶음

우선 새로 정의해서 특정 열을 기준으로 수치를 내림차순하는 함수를 만든다.   

그 전에 데이터프레임을 예시로 만들자면 아래와 같다. 
이름, 키, 점수의 변수를 만들어 이름별 상위 점수를 구하고자한다.   

```python 
import pandas as pd
df = pd.DataFrame({'name':['lee','lee','park','park'],
                  'height':[160,155,190,170],
                  'score':[23,66,44,78]})
df
```

|name|height|score|
|--|--|--|
|lee|160|23|
|lee|155|66|
|park|190|44|
|park|170|78|


이름별 상위 점수 1개를 추출하기 위해서 함수를 지정한다.  

```python
def func(df,column='score',n=1):
    return df.sort_values(by='score',ascending=False)[:n]
 ```
 
 여기서 n=1을 지정해 1개만 뽑고 sort_values를 이용해 숫자를 나열한다.    
 여기서 **ascending=False**는 오름차순 말고 내림차순을 하라는 의미이다.   
 그래서 상위 점수 내림차순해 맨 위에 1개를 추출할 수 있게 된다.   

* Point : 이 함수를 apply에 적용하여 데이터프레임에 적용이 가능

```python
df.groupby('name').apply(func)
```

이름을 그룹핑해서 이름별 상위 점수 1개를 뽑았다.    
그에 따른 결과는 다음과 같다.   

|  |name|height|score|
|--|--|--|--|
|name|  |  |  |				
|lee|lee|155|66|
|park|park|170|78|


## 2. 결측치가 아닌 행만 불러오기
### notnull, isnull함수를 이용하기  

> notnull : Series에서 결측값이 아니면 True, 맞으면 False Boolean값을 나타냄
> isnull : notnull과 반대로 결측치이면 True, 아니면 False값을 나타냄  


새로운 데이터프레임 예시를 들자면 아래와 같습니다. 
```python
df = pd.DataFrame({'name':['lee','lee','park','park'],
                  'height':[160,np.nan,190,170],
                  'score':[23,66,44,np.nan]})
df
```
|name|height|score|
|--|--|--|
|lee|160|23|
|lee|NaN|66|
|park|190|NaN|
|park|170|78|

여기서 결측치가 있는 행을 제외한 데이터프레임만 조회하고자 한다.  

그 때 사용할 수 있는 함수가 notnull이다.   
