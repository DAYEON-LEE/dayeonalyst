---
layout: post
title: "[Programmers] 프로그래머스 lv1 완주하지 못한 선수 "
excerpt: "파이썬을 이용한 알고리즘 풀이"
author: Dayeon Lee
date: 2020-12-30 22:35:00 +0800
tags: [python, Programmers, algorithm]
---


## 1. 프로그래머스 완주하지 못한 선수 문제  
> 마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

**조건**
1. 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
2. completion의 길이는 participant의 길이보다 1 작습니다.
3. 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
4. 참가자 중에는 동명이인이 있을 수 있습니다.


|participant|completion|return|
|--|--|--|
|["leo", "kiki", "eden"]|["eden", "kiki"]|"leo"|
|["marina", "josipa", "nikola", "vinko", "filipa"]|["josipa", "filipa", "marina", "nikola"]|"vinko"|
|["mislav", "stanko", "mislav", "ana"]|["stanko", "ana", "mislav"]|"mislav"|


### 모든 테스트를 통과한 풀이답안

```Python
def solution(participant, completion):
    d = {}
    for x in participant:
        d[x] = d.get(x,0) + 1
    for y in completion:
        d[y] = d[y] - 1
    answer = [a for a,b in d.items() if b > 0]
    answer = answer[0]
    return answer
  ```


이름에 중복이 있는 문제이므로 for문을 돌리는 방법도 있겠지만 시간도 많이 걸리고 효율성이 떨어진다.  
이와 같은 상황에 사용할 수 있는 자료구조는 **해시**이다.  

> **해시** : key(키)와 value(값)를 저장하는 데이터 구조 

- 장점
    1. 데이터 저장 또는 읽는 속도가 빠름 
    2. key에 대한 데이터가 중복확인이 쉬움
- 단점
    1. 저장공간이 많이 필요
    2. 주소가 동일할 경우 충돌가능성 있음 
    
    

여기서 시간 복잡도가 가장 적은 해시라는 자료구조를 이용하는게 Point였다.  
우선 딕셔너리가 해시 구조중에 하나이므로 **d={}를 생성**했다.   

그리고 participant(마라톤 참여자)의 이름을 키로 두고 value값을 get합수를 사용해 이름이 나오면 1씩 더하게끔 했다.   

> 그럼 같은 이름이 중복되어 나와도 value값은 2이상으로 표현되어 구별할 수 있다.  
그리고 completion(완주자)의 이름이 키로 나오면 그 키(완주자 이름)의 value값을 1을 빼면 보통은 값이 0이 된다.  


여기서 상쇄되지 않은 이름이 완주하지 못한 사람으로 나옴을 알 수 있다.   


### collections 모듈 사용한 예시 
 ```Python
 def solution(participant, completion):
    answer = collections.Counter(participant) - collections.Counter(completion)
    return list(answer.keys())[0]

 ```
 
 다른 사람의 코드 예시를 보다가 모듈을 적절히 활용하면 더 쉽게 접근이 가능하다고 느껴 들고왔다.  
 
 흥미로웠던 점은 Counter 즉 딕셔너리끼리 뺄셈이 되어 상쇄가 된다는 점이었다.   
 
 같은 키에 값이 2와 2라면 빼면 0이니 딕셔너리에서 없어지고 2와 1이라면 1이 남아 딕셔너리에도 키와 값이 존재했다. 
 
 > **collections 모듈** : 파이썬의 범용 내장 컨테이너 dict, list, set 및 tuple에 대한 대안을 제공하는 특수 컨테이너 데이터형을 구현
 
 여러가지 객체가 있지만 특히 **Counter**가 매우 유용하게 쓰일 것 같다.  
 
 > Counter 객체 : 편리하게 빠르게 개수를 세어주는 도구 
 
 
 ```Python
# 목록에 있는 단어의 빈도를 집계합니다
cnt = Counter()
for word in ['red', 'blue', 'red', 'green', 'blue', 'blue']:
    cnt[word] += 1
cnt
```

Counter는 word가 나오면 value값으로 1을 더해주고 같은 word가 나오면 반복해 1을 더해준다.   

```
Counter({'blue': 3, 'red': 2, 'green': 1})
```

다음과 같이 결과가 나온다.   
딕셔너리의 형태라는 것을 알 수 있다.   


※ 특히 자연어처리시 빈도수를 체크할 때 유용하게 사용가능하다.   

 ```Python
import re
words = re.findall(r'\w+', open('hamlet.txt').read().lower())
Counter(words).most_common(10)
 ```
 
 여기서 가장 흔한 단어 10개를 Counter를 사용하면 쉽게 찾아줍니다.   
 
 
