---
layout: post
title: "[python] 문자를 날짜로 datetime이용해 변환/그룹별 특정 칼럼의 비율, 누적합, 누적비율계산"
excerpt: "데이터프레임에서 특정함수를 사용해 필요한 데이터를 불러보자."
author: Dayeon Lee
date: 2020-12-29 23:00:00 +0800
tags: [python, groupby,]
---

## 1. 문자를 날짜로 datetime이용해 변환하기
### datetime 모듈이용 

```python 
import pandas as pd
import datetime as dt
a = pd.DataFrame({'date':['2020-01-01','2020-02-11','2020-03-03'],
                 'color':['red','red','blue'],
                 'age': [20,30,40]})
a
```

|--|date|color|age|
|--|--|--|--|
|0|2020-01-01|red|20|
|1|2020-02-11|red|30|
|2|2020-03-03|blue|40|


date의 데이터타입이 여기서 string 즉, 문자열이다.  
그러나 날짜 데이터를 분석할 때에 datetime형으로 타입을 바꿔주면 분석하기 수월하다.   
그래서 데이터타입 변경을 해보자. 

```python 
a['date'] = pd.to_datetime(a['date'])
a.dtypes
```

아래 결과를 보면 date의 타입은 datetime으로 변경된 것을 알 수 있다. 

```
date     datetime64[ns]
color            object
age               int64
dtype: object
```


## 2. 그룹별 특정 칼럼의 값의 , 비율, 누적비율계산하기
### groupby, cumsum, apply함수를 이용하기 

```python 
import pandas as pd
import datetime as dt
a = pd.DataFrame({'date':['2020-01-01','2020-02-11','2020-03-03','2020-04-01'],
                 'color':['red','red','blue','blue'],
                 'age': [20,30,40,70]})
a
```


|--|date|color|age|
|--|--|--|--|
|0|2020-01-01|red|20|
|1|2020-02-11|red|30|
|2|2020-03-03|blue|40|
|3|2020-04-01|blue|70|


위와 같은 데이터프레임을 사용한다고 하자. 
여기서 color별 age의 와 값의 비율 그리고 누적비율을 계산해보자.

```python 
A = a.groupby(['color','age']).size().to_frame()
A = A.reset_index()
A = A.rename(columns={0:'count'})
A['cum_count'] = A.groupby('color')['age'].cumsum(axis=0)
A['norm_count'] = A.groupby('color')['age'].apply(lambda x : x/sum(x))
A['cum_norm_count'] = A.groupby('color')['norm_count'].cumsum(axis=0)
A
```


코드를 해석하자면 

```python 
A = a.groupby(['color','age']).size().to_frame()
A
```


|--|--|0|
|--|--|--|
|color|age|--|	
|blue|40|1|
|--|70|1|
|red|20|1|
|--|30|1|

다음과 같은 프레임이 나온다. 


```python 
A = A.reset_index()
A = A.rename(columns={0:'count'})
A
```
A의 프레임을 인덱스를 초기화시키고 칼럼면 0을 count로 바꾸면 다음과 같다.  


|color|age|count|
|--|--|--|
|0|blue|40|1|
|1|blue|70|1|
|2|red|20|1|
|3|red|30|1|

다음과 같은 데이터프레임을 구할 수 있다. 
여기서 부턴 groupby함수를 사용해 function을 적용하면 된다. 


```python 
A['cum_count'] = A.groupby('color')['age'].cumsum(axis=0)
A['norm_count'] = A.groupby('color')['age'].apply(lambda x : x/sum(x))
A['cum_norm_count'] = A.groupby('color')['norm_count'].cumsum(axis=0)
A
```

우선 cumsum은 color별 age의 합을 더해 누적해준다.  

그리고 color별 age값을 정규화해주는 함수는 apply, lambda를 사용해 x/sum(x)해주어 색깔별 나이의 값이 차지하는 비율을 구한다.  

마지막으로 정규화해 나타낸 비율을 누적합한 것을 데이터프레임에 담았다.   

|--|color|age|count|cum_count|norm_count|cum_norm_count|
|--|--|--|--|--|--|--|
|0|blue|40|1|40|0.363636|0.363636|
|1|blue|70|1|110|0.636364|1.000000|
|2|red|20|1|20|0.400000|0.400000|
|3|red|30|1|50|0.600000|1.000000|

다음과 같은 결과값을 얻을 수 있다. 
