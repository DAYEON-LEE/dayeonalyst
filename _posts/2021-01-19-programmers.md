---
layout: post
title: "[Programmers] 프로그래머스 lv.2 프린터"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-01-19 21:00:00 +0800
tags: [python, algorithm,pop,stack,queue]
---

> 문제 설명
현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.


1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.


- 조건
  1. 현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.
  2. 인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.
  3. location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며 대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.


|priorities|	location|	return|
|--|--|--|
|[2, 1, 3, 2]	|2	|1|
|[1, 1, 9, 1, 1, 1]	|0|	5|


모든 테스트를 통과한 풀이답안

```Python
def solution(priorities, location):
    loc = [i for i in range(len(priorities))]
    fnl_loc = []
    
    while len(priorities) != 0:
        if priorities[0] == max(priorities):
            fnl_loc.append(loc.pop(0))
            priorities.pop(0)
        else:
            priorities.append(priorities.pop(0))
            loc.append(loc.pop(0))
    print(fnl_loc)
    print(loc)
    return fnl_loc.index(location)+1
```






배울점이 많은 다른 사람 풀이 코드 
```Python
def solution(priorities, location):
    queue =  [(i,p) for i,p in enumerate(priorities)]
    answer = 0
    while True:
        cur = queue.pop(0)
        if any(cur[1] < q[1] for q in queue):
            queue.append(cur)
        else:
            answer += 1
            if cur[0] == location:
                return answer
```
