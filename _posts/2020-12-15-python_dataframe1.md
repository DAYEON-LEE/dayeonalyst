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

```python
mask = (df['score'].notnull()) & (df['height'].notnull())
df[mask]
```

mask를 이용해서 score와 height열에 있는 결측치 값의 행을 제거한 데이터프레임을 도출했다.  
반대로 결측치값만 조회하고자한다면 isnull을 사용하면 된다.   

|name|height|score|
|--|--|--|
|lee|160|23|
|park|170|78|

결과는 위와 같다. 완벽히 결측치행들이 제거됨을 볼 수 있다.  
하지만 더 간단한 방법으로 결측치가 있는 모든 행들을 제거할 수 있다.   
그것은 dropna함수를 사용하면 된다.  

```python
df.dropna()
```

|name|height|score|
|--|--|--|
|lee|160|23|
|park|170|78|

dropna함수를 사용하면 위에 notnull을 사용했듯이 같은 결과값을 나타낼 수 있다.  
다만 차이라고 한다면 notnull은 원하는 열만 부분적으로 뽑아낼 수 있고 dropna는 열에 상관없이 모든 열의 결측치가 든 행을 제거한다는 점이다.   


## 3. 정규표현식을 사용해 문자열에서 숫자만 추출하기
### re모듈 함수 findall 이용하기

> findall : 문자열에서 특정문구,부호,숫자등을 찾아서 모두 불러오는 함수

이 문제를 해결하기 위해 임의로 만든 데이터프레임이다.  

```python
df = pd.DataFrame({'x':['11ab','aa44','cdd1f'],
                  'y':[1,2,3]})
df
```

|x|y|
|--|--|
|11ab|1|
|aa44|2|
|cdd1f|3|

여기서 x열의 문자열에서 숫자만 추출해보자.   

```python
df['x'].apply(lambda x : re.findall('\d+',x)[0])
```

변수 x에만 함수를 적용해서 구하면 되기 때문에 apply와 lambda를 사용한다.   
re.findall('\d+',x)부분에서 **\d+**부분은 정수가 1개이상 나열된 것을 불러와라는 의미이다.  
그리고 모든 정수값을 []리스트로 값이 나열되어 나온다.  
그 중 첫 번째로 나온 정수값을 고르기위해 뒤에 [0]을 붙여주었다.    

```
  [Output]
0 11
1 44
2 1 
```

위와 같은 결과값이 나온다.   
