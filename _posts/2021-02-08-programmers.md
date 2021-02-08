---
layout: post
title: "[Programmers] 프로그래머스 lv.2 H-Index"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-08 14:00:00 +0800
tags: [python, algorithm,정렬,sorted,enumerate]
---

> 어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다. 어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

- 조건
  1. 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
  2. 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.


|citations|	return|
|--|--|
|[3, 0, 6, 1, 5]|	3|


모든 테스트 통과 코드 
```Python
def solution(citations):
    citations = sorted(citations)
    l = len(citations)
    for i in range(l):
        if citations[i] >= l-i:
            return l-i
    return 0
```

처음에 내가 낸 코드는 if len(citations) - i >= citations[i] & len(citations) - (len(citations) - i -1 ) <= citations[i] 해서 리스트를 만들어 넣어준 후 max()로 큰 값을 찾아내었다. 
문제를 잘 못 해석한 경우였다.  

sort를 정렬해서 citations의 길이에서 i 즉, 인덱스 값을 빼준 값이 citations[i]값보다 작게하는 l-i값만 구해주면 되는 것이었다. 



