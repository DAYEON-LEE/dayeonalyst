---
layout: post
title: "[python] 중복된 행 조회/삭제, 특정값 대체, 특정값을 포함한 행만 추출"
excerpt: "DataFrame에서 duplicated(), drop_duplicates(), replace(), appplymap(), map(), mapapply()등의 함수를 이용해보자."
author: Dayeon Lee
date: 2020-12-09 19:00:00 +0800
tags: [python, drop_duplicates, replace, apply, map, applymap, duplicated]
---

## 중복된 행 조회 및 삭제 
### 1. duplicated, drop_duplicates 함수를 이용해보자
---
* duplicated() 

|name|age|blood|
|--|--|--|
|정국|24|A|
|진|28|B|
|태형|26|O|
|정국|24|A|
|남준|26|AB|


이런 데이터가 주어진다고 하자. 

> duplicated() : 중복된 행이 나타나면 True 아니면 False를 나타내는 Boolean 마스크 생성 

```python
bts.duplicated()
```

```
0  False
1  False
2  False
3  True
4  False
```

name이 정국인 행과 똑같은 행이 3번째에 또 나와 True값이 나왔다.  
그러나 만약 특정 열만 비교해 중복값을 뽑아내고 싶다면 옵션값에 **subset**을 이용하면 된다. 

> subset['age'] 

```python
bts.duplicated(subset=['age'])
```

```
0  False
1  False
2  False
3  True
4  True
```

subset을 사용해 특정 열 'age'만 보고 같은 행이 있는지 Boolean을 통해 알려준다.  
여기서 나이만 보기 때문에 24인게 3행에 26인게 4행에 같아 True값이 나왔다.  
subset에 여러 열의 값을 넣어 중복된 행을 찾아낼 수도 있다. 

> subset['age','blood'] 

```python
bts.duplicated(subset=['age','blood'])
```

```
0  False
1  False
2  False
3  True
4  False
```

위의 결과값에서 알 수 있듯이 나이와 혈액형을 기준으로 중복된 행은 3번째 행인 것을 알 수 있다. 
나이가 24, 혈액형이 A이 0행과 3행이 값아 2번째로 같은 값이 나온 3행에서 True값이 나왔다.  


* drop_duplicates() 

> drop_duplicates() : 중복된 행들을 제거해주는 함수 

```python
bts.drop_duplicates() 
```
