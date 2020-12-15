---
layout: post
title: "[python] 그룹별 수치 상위 N개 추출/결측치 아닌 행만 추출/문자열에서 숫자만 추출"
excerpt: "데이터프레임에서 특정함수를 사용해 필요한 데이터를 불러보자."
author: Dayeon Lee
date: 2020-12-15 23:00:00 +0800
tags: [python, groupby, sort_values, notnull, isnull, re]
---

## 그룹별 수치 상위 N개 불러오기
### 1. groupby함수와 apply함수 이용하기 

> groupby : 데이터프레임에서 특정 열을 기준으로 데이터를 묶음

우선 새로 정의해서 특정 열을 기준으로 수치를 내림차순하는 함수를 만든다.   

그 전에 데이터프레임을 예시로 만들자면 

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


