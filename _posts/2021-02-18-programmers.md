---
layout: post
title: "[Programmers] 프로그래머스 lv.2 오픈채팅방"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-18 22:00:00 +0800
tags: [python, algorithm,programmers,]
---

테스트를 통과한 풀이 
```Python
def solution(record):
    d = {}
    answer = []
    lst = []
    for i in record:
        rec = i.split(" ")
        if rec[0] == "Leave":
            lst.append([rec[1], "님이 나갔습니다."])
        elif rec[0] == "Enter":
            d[rec[1]] = rec[2]
            lst.append([rec[1], "님이 들어왔습니다."])
        elif rec[0] == "Change":
            d[rec[1]] = rec[2]

    for log in lst:
        answer.append(d[log[0]] + log[1])   
    return answer
```

https://kyome.tistory.com/108의 블로그 코드를 참고했다.  
처음엔 list와 zip, enumerate로 index로 접근해서 풀려고 노력해보았다.   
하지만 코드만 복잡해질 뿐 더 나아지지 않아 1시간이 넘어가자 답안을 보기로 했다.   
아니 딕셔너리로 id를 key로 name을 value로 접근해서 값을 변경하는 방법을 거의 택했다.   
정말 알고리즘을 알고 있어도 문제를 파악하고 어떤 알고리즘을 사용해야할지 빨리 떠올리는게 관건인듯 하다.   
다시 해시를 이용해 푸는 문제들의 특징을 공부하고 알고리즘을 더 연구해야겠다고 생각했다.   
