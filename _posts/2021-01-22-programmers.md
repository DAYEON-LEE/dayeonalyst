---
layout: post
title: "[Programmers] 프로그래머스 lv.2 가장 큰 수"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-01-22 21:00:00 +0800
tags: [python, algorithm,sort,lambda]
---

> 문제 설명
0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.


- 조건
  1. numbers의 길이는 1 이상 100,000 이하입니다.
  2. numbers의 원소는 0 이상 1,000 이하입니다.
  3.정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.


|numbers|return|
|--|--|
|[6, 10, 2]	|"6210"|
|[3, 30, 34, 5, 9]	|"9534330"|	


모든 테스트를 통과한 풀이답안

```Python
def solution(numbers):
    numbers = list(map(str,numbers))
    numbers.sort(key = lambda x : x*3,reverse=True)
    return str(int(''.join(numbers)))
```

permutation(조합)으로 접근하다 시간초과로 sort와 lambda를 이용해서 풀어야겠다는 생각을 했다.    
하지만 그 이상으로 생각이 나지않아 다른 코드 풀이를 참고하였고...
정말 wow 놀라움을 금치 못했다.   왜 난 생각을 못했을까? 싶을정도로 간단하지만 아이디어가 너무 좋았다!(그게 센스라고 생각한다)

숫자를 반복해 길게 늘리고 str을 적용해 내림차순하여 가장 큰 수를 만들어냈다. 

내가 실패한 코드 

```Python
from itertools import permutations 
def solution(num): 
  permute = list(permutations(num,len(num))) 
  list_permute = [''.join(map(str,i)) for i in permute] 
  answer = max(list_permute) 
  return answer
```
조합을 이용한다는 접근은 좋았으니 모든 수를 다 적용해 비교한다는 점에서 시간초과가 되었다.   
