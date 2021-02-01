---
layout: post
title: "[Programmers] 프로그래머스 lv.2 기능개발"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-01 23:00:00 +0800
tags: [python, algorithm,pop]
---

> 먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

- 조건
  1. 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
  2. 작업 진도는 100 미만의 자연수입니다.
  3. 작업 속도는 100 이하의 자연수입니다.
  4. 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.



|progresses	|speeds	|return|
|--|--|--|
|[93, 30, 55]	|[1, 30, 5]	|[2, 1]|
|[95, 90, 99, 99, 80, 99]|	[1, 1, 1, 1, 1, 1]|	[1, 3, 2]|



모든 테스트를 통과한 풀이답안

```Python
def solution(progresses, speeds):
    answer = []
    ans=[]
    for i in range(len(progresses)):
        p= progresses.pop(0)
        s= speeds.pop(0)
        if (100-p)%s==0:
            answer.append((100-p)//s)
        else:
            answer.append((100-p)//s + 1)
    while len(answer) > 0:
        max = answer.pop(0)  
        answer1 = answer.copy()
        num = 1
        for j in range(len(answer)):
            if max >= answer[j]:
                num+=1
                answer1.pop(0)
            else:
                break
        ans.append(num)   
        answer = answer1.copy()
    return ans
```



다른 사람의 풀이

```Python
def solution(progresses, speeds):
    Q=[]
    for p, s in zip(progresses, speeds):
        if len(Q)==0 or Q[-1][0]<-((p-100)//s):
            Q.append([-((p-100)//s),1])
        else:
            Q[-1][1]+=1
    return [q[1] for q in Q]
```
 
