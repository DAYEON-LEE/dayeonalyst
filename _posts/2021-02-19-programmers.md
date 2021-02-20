---
layout: post
title: "[Programmers] 프로그래머스 lv.2 스킬트리"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-19 13:00:00 +0800
tags: [python, algorithm,programmers]
---
 
 
1차시도 (런타임에러)
```Python
def solution(skill, skill_trees):
    answer = 0
    included = ''
    lst = []
    for i in skill_trees:
        for j in i:
            if j in skill:
                included+=j
        lst.append(included)
        included = ''
    for k in lst:
        if (k not in skill) or (k[0] != skill[0]):
            answer -=1
    return len(skill_trees) + answer 
```

정답은 맞으나 런타임오류가 떠서 통과하지 못했다.  
아무래도 for로 계속 접근하는 것도 있지만 append와 string 문자 하나하나에 접근해서 그런게 아닐까 생각하고 있다. 


테스트 통과한 코드 
```Python
def solution(skill, skill_trees):
    skill = list(skill)
    flag=[]
    for i in skill_trees:
        post_skill_trees = []
        for j in list(i):
            if j in skill:
                post_skill_trees.append(j)
        for idx, j in enumerate(post_skill_trees):
            if j != skill[idx]:
                flag.append(-1)
                break
    return len(skill_trees)+sum(flag)
```
그리고 string을 바로 list로 넣어 알파벳 하나하나를 리스트에 바로 넣어 접근하는 코드를 발견했다. 처음 내가 짠 코드랑 별 다를게 없어 보였는데 enumerate로 index값과 알파벳값을 비교해 skill순서에 해당되지 않으면 -1을 빼주었다.   


다른 사람 풀이 
```Python
def solution(skill, skill_trees):
    answer = 0

    for skills in skill_trees:
        skill_list = list(skill)

        for s in skills:
            if s in skill:
                if s != skill_list.pop(0):
                    break
        else:
            answer += 1

    return answer
```
pop을 이용한 풀이를 발견하였는데 처음엔 pop으로 풀어볼까 했지만 어떻게 접근해야할지 망설여져서 직접 코드를 짜지 못했는데 다른 사람 풀이의 대표 예시로 올라와 한 수 또 배워간다. 다양한 알고리즘을 효율적으로 적재적소에 쓰는 날을 꿈꾸며..
