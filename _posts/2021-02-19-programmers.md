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
