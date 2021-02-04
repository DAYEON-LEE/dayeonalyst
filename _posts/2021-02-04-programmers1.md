---
layout: post
title: "[Programmers] 프로그래머스 lv.2 타겟넘버"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-04 22:00:00 +0800
tags: [python, algorithm,완전탐색, DFS]
---

> 사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

- 조건
  1. 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
  2. 각 숫자는 1 이상 50 이하인 자연수입니다.
  3. 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

|numbers|	target	|return|
|--|--|--|
|[1, 1, 1, 1, 1]	|3	|5|

모든 테스트 통과 코드 (완전탐색)
```Python
from itertools import product
def solution(numbers, target):
    l = [(x, -x) for x in numbers]
    s = list(map(sum, product(*l)))
    return s.count(target)
```

모든 테스트 통과 코드 (DFS)    
```Python
def iterative_solution(numbers, target):
    result_list = [0]    
    for i in range(len(numbers)):
        temp_list = []
        for j in range(len(result_list)):
            temp_list.append(result_list[j] - numbers[i])
            temp_list.append(result_list[j] + numbers[i])
        result_list = temp_list
        print(result_list)
    return result_list.count(target)
```



