---
layout: post
title: "[Programmers] 프로그래머스 lv.2 최솟값 만들기"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-25 09:00:00 +0800
tags: [python, algorithm,programmers]
---

문제 
> 배열 A, B에서 각각 한 개의 숫자를 뽑아 두 수를 곱합니다. 이러한 과정을 배열의 길이만큼 반복하며, 두 수를 곱한 값을 누적하여 더합니다. 이때 최종적으로 누적된 값이 최소가 되도록 만드는 것이 목표입니다. (단, 각 배열에서 k번째 숫자를 뽑았다면 다음에 k번째 숫자는 다시 뽑을 수 없습니다.)

제한사항 
- 배열 A, B의 크기 : 1,000 이하의 자연수
- 배열 A, B의 원소의 크기 : 1,000 이하의 자연수

|A	|B	|answer|
|--|--|--|
|[1, 4, 2]|	[5, 4, 4]|	29|
|[1,2]|	[3,4]	|10|


테스트 통과한 코드 
```Python
def solution(A,B):
    answer = 0
    A.sort()
    B.sort(reverse=True)
    
    for i in range(len(A)):
        answer += A[i]*B[i]

    return answer
```
