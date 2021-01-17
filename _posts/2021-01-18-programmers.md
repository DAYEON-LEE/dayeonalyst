---
layout: post
title: "[Programmers] 프로그래머스 lv.2 더 맵게"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-01-18 00:15:00 +0800
tags: [python, algorithm,heap, heapq]
---

> 문제 설명
매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.
섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)

- 조건
  1. scoville의 길이는 2 이상 1,000,000 이하입니다.
  2. K는 0 이상 1,000,000,000 이하입니다.
  3. scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
  4. 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.
  
  
|scoville|	K|	return|
|--|--|--|
|[1, 2, 3, 9, 10, 12]		|7		|	2|


모든 테스트를 통과한 풀이답안

```Python
import heapq
def solution(scoville, K):
    answer = 0
    heapq.heapify(scoville)
    print(scoville)
    while scoville[0] < K:
        try:
            heapq.heappush(scoville,heapq.heappop(scoville)+heapq.heappop(scoville)*2)
            answer +=1
        except IndexError:
            return -1
    return answer
```

처음엔 heapq 모듈을 사용하지 않고, sort, pop, insert함수를 사용해 답을 구했다.  
하지만 정확성은 100%가 나왔으나 효율성을 통과하지 못했다.   


그리고 찾아보니 heap은 이진트리구조로 O(log n)으로 heapify를 이용해 정렬하는 것이 sort보다 빠르다는 것을 알게 되었다.  

> heapq 자료구조 : 인덱스 0에서 시작해 k번째 원소가 항상 자식 원소들 (2k+1, 2k+2)보다 작거나(크거나) 같은 최소힙으로 정렬 



- heapq 함수 
  1.heappush(heap,item) : item을 heap에 추가 
  2.heappop(heap) : heap에서 가장 작은 원소를 pop해서 return, 비어있는 경우 IndexError가 호출됨
  3.heapify(x) : 리스트 x를 heap으로 변환 
