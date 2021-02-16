---
layout: post
title: "[Programmers] 프로그래머스 lv.2 큰 수 만들기"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-15 12:00:00 +0800
tags: [python, algorithm]
---

> 문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

- 조건
  1. number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
  2. k는 1 이상 number의 자릿수 미만인 자연수입니다.

|number|	k	|return|
|--|--|--|
|1924	|2	|94|
|1231234	|3|	3234|
|4177252841	|4	|775841|


1차 시도 (시간초과)
```Python
def solution(number, k):
    from itertools import combinations
    lst = []
    a = list(combinations(range(len(number)),k))
    for i in a:
        lst.append("".join([number[j] for j in range(len(number)) if j not in i]))
    return max(lst)
```

다른 사람 풀이
```Python
def solution(number, k):
    stack = [number[0]]
    for num in number[1:]:
        while len(stack) > 0 and stack[-1] < num and k > 0:
            k -= 1
            stack.pop()
        stack.append(num)
    if k != 0:
        stack = stack[:-k]
    return ''.join(stack)
```

하나씩 값을 stack에 쌓으면서 큰 값이 나오면 pop하고 그 다음 값을 append해주면서 큰 값을 list에 담는 방식이다.    
그리고 k가 0이 되지 않고 끝이 난다면 마지막은 작은 값들만 들어가 있으므로 첫 번째꺼부터 k까지 슬라이싱해서 구하면 된다.     

여기서 관점은 while문과 조건문 그리고 stack을 잘 활용해서 코드가 완성되었다는 점이며 이런 원리를 떠올린 것이 대단하다고 느꼈다. 
나도 computing thinking을 더욱 더 발전시키고 싶다.   화이팅 !! 


### 느낀점
아무래도 알고리즘을 접한지 얼마되지 않았고, 주로 데이터를 pandas중심적으로 다루다보니 stack을 떠올리지 못했다. 
시간 복잡도가 itertools의 경우 높아 시간이 지연되는 점으로 combinations로 푸는 시도는 시간초과로 끝이 났다.   
그래서 다른 사람의 풀이를 보고 계속 이 알고리즘이 왜 돌아가고 어떤 원리인가를 공부하면서 30분간 뜯어보며 이제 좀 이해했다.   
하지만 내가 비슷한 문제가 나왔을 때 stack을 떠올려 풀 수 있을지 걱정이지만 계속 잊지 않도록 이해하면서 코드를 풀이해야겠다 생각했다.     

