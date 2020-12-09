---
layout: post
title: "[python] 중복된 행 조회/삭제, 특정값 대체, 특정값을 포함한 행만 추출"
excerpt: "DataFrame에서 duplicated(), drop_duplicates(), replace(), appplymap(), map(), mapapply()등의 함수를 이용해보자."
author: Dayeon Lee
date: 2020-12-09 20:00:00 +0800
tags: [python, drop_duplicates, replace, apply, map, applymap, duplicated]
---

## 1. 중복된 행 조회 및 삭제 
###  duplicated, drop_duplicates 함수를 이용해보자
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


  [Output]
|name|age|blood|
|--|--|--|
|정국|24|A|
|진|28|B|
|태형|26|O|
|남준|26|AB|


옵션을 주지 않고 기본 함수를 사용하면 모든 열의 값이 동일한 행을 삭제해준다.    
그래서 이름이 전국인 행 전체가 사라진 것을 위와 같이 볼 수 있다.    


> drop_duplicates(['age'], keep = 'first') 

```python
bts.drop_duplicates(['age'], keep = 'first') 
```


  [Output]
|name|age|blood|
|--|--|--|
|정국|24|A|
|진|28|B|
|태형|26|O|


옵션 keep = 'first'를 주면 중복된 값이 처음으로 나오는 행만 남겨두고 삭제하라는 의미이다.   
그래서 나이는 26으로 태형, 남준이가 같았지만 처음으로 나온 태형의 행이 남은 것을 알 수 있다.     
반대로 keep = 'last'를 주면 마지막에 나온 행이 남을 것이다.    


## 2. 데이터프레임에서 특정 열의 특정 값들을 대체
### replace, apply 함수를 이용해보자

> replace() : Series에 특정값을 다른 값으로 

```python
bts['name'] = bts['name'].replace({'진':'슈가'})
bts
```


  [Output]
|name|age|blood|
|--|--|--|
|정국|24|A|
|슈가|28|B|
|태형|26|O|
|정국|24|A|
|남준|26|AB|


replace함수를 사용해 name에서 진을 슈가로 값을 대체하고 데이터프레임을 확인해보니 변경되었음을 알 수 있다.    

또 다른 방법으로는 **apply**함수를 사용하는 것이다.    
주로 저는 이 방법을 많이 사용하는데 그 이유는 단지 값을 일일이 replace처럼 바꾸는게 아니라 열을 원하는 방향으로 한 번에 변경해주기 때문이다.    
예를 들면 age에 3씩 더해주거나 name뒤에 문자열을 추가할 수 있다.    

> bts['age'] = bts['age'].apply(lambda x : x + 3)   

```python
bts['age'] = bts['age'].apply(lambda x : x + 3) 
bts
```


  [Output]
|name|age|blood|
|--|--|--|
|정국|27|A|
|슈가|31|B|
|태형|29|O|
|정국|27|A|
|남준|29|AB|


age가 3씩 증가함을 볼 수 있다.   

> bts['name'] = bts['name'].apply(lambda x : x + '귀여워')

```python
bts['name'] = bts['name'].apply(lambda x : x + ' 귀여워')
bts
```


  [Output]
|name|age|blood|
|--|--|--|
|정국 귀여워|27|A|
|슈가 귀여워|31|B|
|태형 귀여워|29|O|
|정국 귀여워|27|A|
|남준 귀여워|29|AB|


숫자뿐만 아니라 문자열도 변경하는게 가능하다.   
이 밖에도 함수를 다양하게 적용할 수 있고 데이터프레임 열을 같은 형식으로 한 번에 바꾼다는 장점이 있다.    


### 이 밖에서 map, applymap 함수를 사용할 수 있다 

> map() : 1차원 원소별 적용하고 리스트로도 반환이 가능 

> bts['age'].map(lambda x : x+100)

```python
bts['age'].map(lambda x : x+100)
bts
```


  [Output]
|name|age|blood|
|--|--|--|
|정국 귀여워|127|A|
|슈가 귀여워|131|B|
|태형 귀여워|129|O|
|정국 귀여워|127|A|
|남준 귀여워|129|AB|


apply함수와 같이 age에 100을 더 한 값이 나옴을 볼 수 있다.    
다만   
* apply와 map의 차이   

> apply는 **데이터프레임 행별, 열별**에 적용이 가능
> But, map의 경우 **1차원 원소별**에만 적용이 가능 


> applymap() : 2차원 데이터프레임 구조의 원소별 적용   

그래서 만약 BTS.applymap(lambda x : x + 100)을 사용하면 데이터프레임 전체에 숫자 100을 더할려고 할 것이다.    
그러나 문자열엔 숫자연산이 적용되지 않아 ERROR가 뜬다.   
그 점을 유의해면서 applymap함수는 사용해야 한다.       
