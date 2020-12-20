---
layout: post
title: "[Programmers] 프로그래머스 lv1 실패율 "
excerpt: "파이썬을 이용한 알고리즘 풀이"
author: Dayeon Lee
date: 2020-12-20 22:35:00 +0800
tags: [python, Programmers, algorithm]
---


## 1. 프로그래머스 실패율 문제  
> 전체 스테이지의 개수 N, 게임을 이용하는 사용자가 현재 멈춰있는 스테이지의 번호가 담긴 배열 stages가 매개변수로 주어질 때, 
실패율이 높은 스테이지부터 내림차순으로 스테이지의 번호가 담겨있는 배열을 return 하도록 solution 함수를 완성하라.

- 실패율 : 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수

**조건**
1. 단, N + 1 은 마지막 스테이지(N 번째 스테이지) 까지 클리어 한 사용자를 나타낸다.
2. 만약 실패율이 같은 스테이지가 있다면 작은 번호의 스테이지가 먼저 오도록 하면 된다.
3. 스테이지에 도달한 유저가 없는 경우 해당 스테이지의 실패율은 0 으로 정의한다.


|N|stages|result|
|--|--|--|
|5|[2, 1, 2, 6, 2, 4, 3, 3]|[3,4,2,1,5]|
|4|[4,4,4,4,4]|[4,1,2,3]|


### 시간초과, 런타임 에러 (초기 제출안)

```Python
def solution(N, stages):
    answer = []
    fail_ratio = []
    index = []
    length = len(stages)
    num = 0
    for x in range(1,N+1):
        if length != 0 :
            for y in stages:
                if x==y:
                    num+=1
                elif x not in stages:
                    num=0
        else:
            num=0
        fail_ratio.append(num/length)
        length = length - num
        num = 0 
        index.append(x)
    answer = list(zip(index,fail_ratio))
    answer = sorted(answer,key=lambda x : x[1],reverse=True)
    answer = list(c for c,d in answer)
    return answer
```

답안결과는 나왔지만 시간초과와 런타임에러와 마주했던 답안이다.  
우선 필요없는 문법과 자료구조가 있었던 것으로 판단되었다.  

length길이에 대한 조건문은 필요없었고, index 리스트를 따로 만들어서 곧이 zip으로 다시 묶는 과정에서 시간이 많이 소요된 것으로 보였다.  


그 부분을 간단화하기 위해서 고친 답안이 아래와 같다.   


### 모든 테스트를 통과한 풀이답안

```Python
def solution(N, stages):
    answer = []
    length = len(stages)
    num = 0
    for x in range(1,N+1):
        for y in stages:
            if x==y:
                num+=1
        if num > 0:
            answer.append(num/length)
            length = length - num
            num = 0
        else:
            answer.append(0)
    answer = sorted(range(len(answer)),key=lambda k : answer[k],reverse=True)
    answer = [x+1 for x in answer]
    return answer
  ```
  
index와 fail_ratio를 굳이 만들필요 없이 바로 answer리스트에 실패율을 넣어주면 되었다.   
  
  
그리고 num에 조건문을 붙여줘 x==y가 나온 횟수 num에 따라서 stages에 나온 단계 횟수만 실패율을 바로 구하고 아닌 것들은 실패율에 0을 넣어주었다.  
  
그렇게 num=0으로 초기화하면서 반복문을 실행하였다. 
훠씬 코드가 깔끔하고 정리된 느낌이 초안보다 있다는 것을 깨달았다.  
그리고 sorted와 lambda함수를 적용해 실패율순으로 값을 정돈하였다.   


아직 알고리즘에 대한 개념이 잘 잡혀져있지 않아 효율적인 코드란 어떤 것인지는 잘 모르겠다.


그래서 어떻게하면 효율적이고 간단하고 가독성이 좋은 코드를 만들 수 있을까라는 고민을 계속하고 공부하며 블로그를 계속 이어갈 생각이다.   

