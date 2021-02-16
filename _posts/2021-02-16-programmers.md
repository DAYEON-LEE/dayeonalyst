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

