---
layout: post
title: "[Programmers] 프로그래머스 lv1 행렬의 덧셈 "
excerpt: "파이썬을 이용한 알고리즘 풀이"
author: Dayeon Lee
date: 2021-01-12 22:35:00 +0800
tags: [python, Programmers, algorithm, zip]
---


## 1. 프로그래머스 행렬의 덧셈 문제  
> 행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 서로 더한 결과가 됩니다. 2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, solution을 완성해주세요.


**조건**
1. 행렬 arr1, arr2의 행과 열의 길이는 500을 넘지 않습니다.



|n|return|
|--|--|
|12345|[5,4,3,2,1]|

|arr1|	arr2|	return|
|--|--|--|
|[[1,2],[2,3]]	|[[3,4],[5,6]]	|[[4,6],[7,9]]|
|[[1],[2]]	|[[3],[4]]	|[[4],[6]]|


### 모든 테스트를 통과한 풀이답안

```Python
def solution(arr1, arr2):
    answer =[]
    for a,b in zip(arr1,arr2):
        answer.append([c+d for c,d in zip(a,b)])
    return answer
  ```

여기서 **key point**는 zip함수를 떠오르는 것이다.   
그 이유는 같은 index값들의 연산을 해 같은 위치에 리스트에 append해줘야하기 때문이다.    

처음에는 어떻게 이중 리스트안에 넣을 수 있을까 고민하다 이중 for문을 돌리다 실패하였다.   

그러다가 리스트에 덧셈이 된 리스트를 바로 append하는 방식을 취했다.   

그러기위해선 이중 for문이 필요하지만 값을 더해서 바로 리스트로 뽑아낼 수 있는 
**리스트 컴프리헨션** 반복문인 [표현식 for 항목 in 반복 가능한 객체]를 사용했다.   

