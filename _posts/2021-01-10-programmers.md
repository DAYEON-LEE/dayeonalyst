---
layout: post
title: "[Programmers] 프로그래머스 lv1 자연수 뒤집어 배열로 만들기/정수 내림차순으로 배치하기 "
excerpt: "파이썬을 이용한 알고리즘 풀이"
author: Dayeon Lee
date: 2021-01-10 22:35:00 +0800
tags: [python, Programmers, algorithm, sort, map, list, reversed, join]
---


## 1. 프로그래머스 자연수 뒤집어 배열로 만들기 문제  
> 자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.

**조건**
1. n은 10,000,000,000이하인 자연수입니다.



|n|return|
|--|--|
|12345|[5,4,3,2,1]|



### 모든 테스트를 통과한 풀이답안

```Python
def solution(n):
    answer = []
    answer = [int(i) for i in str(n)][::-1]
    return answer
  ```

여기서 **keypoint code**는 [int(i) for i in str(n)][::-1]이다. 
for구문에서 뽑은 요소를 바로 리스트에 꽂아버리는 멋진 코드! 

그리고 [start:end:step]으로 -1을 하면 리스트를 거꾸로 뒤집어 배열하라라는 의미이다. 

하지만 이렇게 말고 다른 사람 풀이에서   
list(map(int,reversed(str(n))))의 코드를 보았다.   

> list(map(함수, 리스트값)) : 리스트값의 요소에 특정 함수를 적용시켜줌

for반복문으로 list의 요소 하나하나 접근하는 것보다 빠르고 간단하게 표현할 수 있다.   



----------------------

## 2. 프로그래머스 정수 내림차순으로 배치하기 문제  
> 함수 solution은 정수 n을 매개변수로 입력받습니다. n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 예를들어 n이 118372면 873211을 리턴하면 됩니다.

**조건**
1. n은 1이상 8000000000 이하인 자연수입니다.



|n|return|
|--|--|
|118372|873211|



### 모든 테스트를 통과한 풀이답안

```Python
def solution(n):
    answer = [i for i in str(n)]
    answer.sort(reverse=True)
    answer = ''.join(answer)
    return int(answer)
  ```

리스트에서 숫자로 된 문자열의 배열또한 sort로 배열할 수 있었다. 
sort합수에서 reverse=True로 내림차순이라는 옵션을 지정해주고 join함수를 사용해 다시 문자를 배합해 integer로 변경했다.   

어렵진 않지만 기본 문법을 정확히 알고 있어야만 빠르게 풀 수 있는 문제였다.   
