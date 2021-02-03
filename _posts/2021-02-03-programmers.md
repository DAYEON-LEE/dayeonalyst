---
layout: post
title: "[Programmers] 프로그래머스 lv.2 전화번호 목록"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-03 14:00:00 +0800
tags: [python, algorithm]
---

> 전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

- 조건
  1. phone_book의 길이는 1 이상 1,000,000 이하입니다.
  2. 각 전화번호의 길이는 1 이상 20 이하입니다.

|phone_book|	return|
|--|--|
|[119, 97674223, 1195524421]	|false|
|[123,456,789]|	true|
|[12,123,1235,567,88]|	false|


정확성 실패/효율성 통과 코드 (1차시도)
```Python
def solution(phone_book):
    answer = True
    lst = []
    from collections import Counter
    for i in phone_book:
        lst.append(i[0])
    for a,b in Counter(lst).items():
        if b == 1:
            continue
        else:
            answer = False
            break
        answer = True
    return answer
```

모든 테스트 통과 코드 (n차 시도)    
```Python

```
