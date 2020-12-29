---
layout: post
title: "[python] 문자를 날짜로 datetime이용해 변환/그룹별 특정 칼럼의 값 비율, 누적합, 누적비율계산"
excerpt: "데이터프레임에서 특정함수를 사용해 필요한 데이터를 불러보자."
author: Dayeon Lee
date: 2020-12-29 23:00:00 +0800
tags: [python, groupby]
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


## 2. 그룹별 특정 칼럼의 값의 수, 비율, 누적비율계산하기
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
여기서 color별 age의 수와 값의 비율 그리고 누적비율을 계산해보자.

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
