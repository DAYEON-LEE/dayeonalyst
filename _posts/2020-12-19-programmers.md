---
layout: post
title: "[Programmers] 프로그래머스 lv1 두개 뽑아서 더하기 "
excerpt: "파이썬을 이용한 알고리즘 풀이"
author: Dayeon Lee
date: 2020-12-19 14:00:00 +0800
tags: [python, Programmers, algorithm,]
---


## 1. 프로그래머스 두개 뽑아서 더하기 문제  
> 정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

### 모든 테스트 통과 답안 

```Python
def solution(numbers):
    answer = []
    for i in range(len(numbers)):
        for j in range(i+1,len(numbers)):
            if (numbers[i]+numbers[j] not in answer):
                answer.append(numbers[i]+numbers[j])
    answer = sorted(answer)
    return answer
```

nC2의 조합 combination을 이용해서 풀 수도 있지만 그러한 함수를 알지 못할 때도 내가 아는 기본 함수들을 이용해서 풀어낼 능력이 필요하다고 생각한다.  
그래서 for 반복구문을 이용해서 문제를 풀었다.  

예를 들면 a = [10,20,30] 이라는 리스트가 있다고 하자.  
a에서 하나씩 꺼내 수를 더한 값들을 중복제거 후 오름차순해야한다.   
그렇다면 계산해야하는 과정은 

- a[0]+a[1], a[0]+a[2]
- a[1]+a[2]

그래서 첫 번째 for 구문에선 첫 번째 인덱스로 0~2까지 돌고 두 번째 for구문에선 0일 때 1~2까지 순환 1일 때는 2만 순환하며 값을 더해 리스트에 더해준다.  

특히 중복을 제거하기위해서 두 수의 합이 중복된 값을 넣으면 append하지 않도록 if 조건문을 설정해주었다.   

하지만 중복제거로는 set함수를 이용할 수 있었으나 리스트에서 어떻게 변환해야하는지 기억이 나지않아 사용하지 못하였다.  
그래서 sorted()는 리스트를 순서대로 정렬해주는데 옵션으로 reverse=True지정하면 내림차순이 된다. 

영기서 sort(), sorted()의 차이를 설명하자면   

> sort() : 리스트의 원본을 변경해 정렬된 값들을 그대로 저장 
> sorted() : 리스트의 원본은 유지하고 리스트를 정렬하는 방법


### set을 이용한 풀이 (다른 사람 문제 답안)

```Python
def solution(numbers):
    answer = []
    for i in range(len(numbers)):
        for j in range(i+1, len(numbers)):
            answer.append(numbers[i] + numbers[j])
    return sorted(list(set(answer)))
  ```

다른 풀이중에 가장 간단 명료한 답안이라 생각되어 들고왔다.  
sorted와 set을 이용해 최대한 간단하게 코드를 만들어낸 점이 인상깊다.  
내가 원하는 방식의 코드 풀이라 기억해두기위해 블로그에 이렇게 적어본다.   

우선 set함수를 사용하면 딕셔너리 형태 {}로 중복된 값을 자동 삭제해준다.  
하지만 리스트값으로 결과값을 배출해야하므로 list함수를 적용시켜 리스트로 뽑아내고 sorted함수를 적용해 바로 오름차순으로 변경한다.

계속 공부하면서 이러한 구조와 함수를 기억하고 익숙해져야겠다. 
