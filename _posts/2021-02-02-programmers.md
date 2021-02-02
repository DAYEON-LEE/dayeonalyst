---
layout: post
title: "[Programmers] 프로그래머스 lv.2 다리를 지나는 트럭"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-02 23:00:00 +0800
tags: [python, algorithm,pop,while,append]
---

> solution 함수의 매개변수로 다리 길이 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.


- 조건
  1. bridge_length는 1 이상 10,000 이하입니다.
  2. weight는 1 이상 10,000 이하입니다.
  3. truck_weights의 길이는 1 이상 10,000 이하입니다.
  4. 모든 트럭의 무게는 1 이상 weight 이하입니다.



|bridge_length	|weight|	truck_weights|	return|
|--|--|--|--|
|2	|10	|[7,4,5,6]	|8|
|100|	100	|[10]	|101|
|100	|100	|[10,10,10,10,10,10,10,10,10,10]	|110|



모든 테스트를 통과한 풀이답안

```Python
def solution(bridge_length, weight, truck_weights):
    answer = 0
    bridge = [0]*bridge_length
    while len(bridge) != 0:
        bridge.pop(0)
        answer +=1
        if truck_weights:
            if sum(bridge)+truck_weights[0] <= weight:
                bridge.append(truck_weights.pop(0))
            else:
                bridge.append(0)
    return answer
```

pop, append를 사용하여 트럭을 한칸씩 옮기면서 시간을 재는 방법을 택했다.   
이런 아이디어는 생각했으나 [0,0,...0]을 bridge_length만큼 만들어 pop하구 트럭 무게값을 넣어주고 못 넣을 경우는 0을 대신 넣어 길이를 유지해주었다.    

그리고 모든 트럭이 다 빠져나오면 pop함수를 이용해 while문을 돌게하고 time을 시간을 재주었다.      
