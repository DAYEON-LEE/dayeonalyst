---
layout: post
title: "[Programmers] 프로그래머스 lv.2 위장"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-01-28 21:00:00 +0800
tags: [python, algorithm,collections,counter]
---

> 스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.


- 조건
  1. clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
  2. 스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
  3.같은 이름을 가진 의상은 존재하지 않습니다.
  4. clothes의 모든 원소는 문자열로 이루어져 있습니다.
  5. 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '_' 로만 이루어져 있습니다.
  6. 스파이는 하루에 최소 한 개의 의상은 입습니다.



|clothes	|return|
|--|--|
|[[yellow_hat, headgear], [blue_sunglasses, eyewear], [green_turban, headgear]]	|5|
|[[crow_mask, face], [blue_sunglasses, face], [smoky_makeup, face]]|	3|



모든 테스트를 통과한 풀이답안

```Python
def solution(clothes):
    from collections import Counter
    counter = Counter([key for cloth, key in clothes])
    value = 1
    for key in counter:
        value *= (counter[key]+1)
    return value-1
```



같은 의상의 종류일 경우를 제외하고 모든 경우의 조합의 수를 구해야했다.   

예를들면 (노란 모자, 머리) (파란 안경, 눈) (검은 캡모자, 머리)가 있다고 하자.    
그럼 모든 경우의 수는 머리의 경우 2가지의 경우가 있고 2가지 중 1가지만 입을 수 있다.   

그렇다면 아예 안입거나 노란 모자만 입거나 검은 캡모자만 입거나 **총 3가지의 경우**
눈의 경우 파란안경을 아예 안쓰거나 파란안경만 쓰거나 **총 2가지의 경우 **

그럼 경우의 수를 구할 때 3*2인데 둘다 안입는 경우는 제외해야하므로 -1을 해준 값이 답이 된다.   


다른 사람의 풀이

```Python
def solution(clothes):
    from collections import Counter
    from functools import reduce
    cnt = Counter([kind for name, kind in clothes])
    answer = reduce(lambda x, y: x*(y+1), cnt.values(), 1) - 1
    return answer
```
 
다른 사람의 풀이에서 for를 사용하지 않고 바로 **reduce함수**를 이용해서 구한 것을 보았다.   
reduce는 중복되지 않도록 값을 계산해주는 함수이다.   

reduce(함수식, 값 , 초기값)으로 예를들면 reduce(lambda x+1, [1,2],0)이면 초기값이 0이고    
1+1 = 2    
2+2 = 4   
결국 4가 최종값이 된다.     
