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

> 해시 : key(키)와 value(값)를 저장하는 데이터 구조 

- 장점
    1. 데이터 저장 또는 읽는 속도가 빠름 
    2. key에 대한 데이터가 중복확인이 쉬움
- 단점
    1. 저장공간이 많이 필요
    2. 주소가 동일할 경우 충돌가능성 있음 
    
    

여기서 시간 복잡도가 가장 적은 해시라는 자료구조를 이용하는게 <span style="color:blue">Poin</span>였다.  
우선 딕셔너리가 해시 구조중에 하나이므로 d={}를 생성했다.   

그리고 participant(마라톤 참여자)의 이름을 키로 두고 value값을 get합수를 사용해 이름이 나오면 1씩 더하게끔 했다.   

그럼 같은 이름이 중복되어 나와도 value값은 2이상으로 표현되어 구별할 수 있다.  
그리고 completion(완주자)의 이름이 키로 나오면 그 키(완주자 이름)의 value값을 1을 빼면 보통은 값이 0이 된다.   
여기서 상쇄되지 않은 이름이 완주하지 못한 사람으로 나옴을 알 수 있다.   



### collections 모듈 사용한 예시 
 ```Python
 def solution(participant, completion):
    answer = collections.Counter(participant) - collections.Counter(completion)
    return list(answer.keys())[0]

 ```
 
 다른 사람의 코드 예시를 보다가 모듈을 적절히 활용하면 더 쉽게 접근이 가능하다고 느껴 들고왔다.  
 
 
