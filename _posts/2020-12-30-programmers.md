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
