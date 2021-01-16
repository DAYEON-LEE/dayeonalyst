---
layout: post
title: "[Programmers] 프로그래머스 lv1 콜라츠 추측 "
excerpt: "파이썬을 이용한 알고리즘 풀이"
author: Dayeon Lee
date: 2021-01-12 22:35:00 +0800
tags: [python, Programmers, algorithm, for, while]
---


## 1. 프로그래머스 행렬의 덧셈 문제  
>예를 들어, 입력된 수가 6이라면 6→3→10→5→16→8→4→2→1 이 되어 총 8번 만에 1이 됩니다. 위 작업을 몇 번이나 반복해야하는지 반환하는 함수, solution을 완성해 주세요. 단, 작업을 500번을 반복해도 1이 되지 않는다면 –1을 반환해 주세요. 


1-1. 입력된 수가 짝수라면 2로 나눕니다. 
1-2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다.
2. 결과로 나온 수에 같은 작업을 1이 될 때까지 반복합니다.



**조건**
1. 입력된 수, num은 1 이상 8000000 미만인 정수입니다.



|n|result|
|--|--|
|6|8|
|16|4|
|626331|-1|


### 모든 테스트를 통과한 풀이답안

```Python
def solution(num):
    answer = 0 
    if num ==1:
        return 0
    while True:
        answer = answer + 1
        num = num/2 if num%2==0 else (num*3)+1
        if num == 1:
            return answer
        elif answer == 500:
            return -1
  ```

문제를 정확히 이해하는 것과 while을 제어하는 법을 알아야 풀 수 있었다.   
우선 while은 조건이 만족될 때까지 계속해서 반복하는 문이라 break문을 걸거나 원하는 값이 나오면 바로 return해주어야한다.       

하지만 여기서 **key point**는 반복을 500번해도 원하는 값이 안나오면 무조건 -1을 뱉어내는 것이다.   
그래서 answer를 반복문을 돌릴 때마다 1을 추가해 500이되면 자동으로 -1을 return하게 했다.    

그리고 만약 처음부터 값이 1이라면 반복문을 돌릴 필요없으므로 바로 0을 return하는 문장을 만드는 것이 중요했다.    
