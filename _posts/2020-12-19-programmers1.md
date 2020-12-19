---
layout: post
title: "[Programmers] 프로그래머스 lv1 내적 "
excerpt: "파이썬을 이용한 알고리즘 풀이"
author: Dayeon Lee
date: 2020-12-19 14:45:00 +0800
tags: [python, Programmers, algorithm, zip, sum]
---


## 1. 프로그래머스 내적 문제  
> 길이가 같은 두 1차원 정수 배열 a, b가 매개변수로 주어집니다. a와 b의 내적을 return 하도록 solution 함수를 완성해주세요.
이때, a와 b의 내적은 a[0]*b[0] + a[1]*b[1] + ... + a[n-1]*b[n-1] 입니다. (n은 a, b의 길이)


### 모든 테스트 통과 답안 

```Python
def solution(a, b):
    answer = 0 
    for i in range(len(a)):
        number = a[i]*b[i]
        answer = number+answer
    return answer
```

내적은 리스트의 인덱스가 같아야 가능하다.  
그래서 a의 인덱스 길이를 이용해 값을 각각 곱해 덧셈연산을 더해 결과값을 구했다. 

상당히 간단한 방법이지만 zip과 sum의 함수를 사용하면 더 간단히 표현할 수 있다.


### set을 이용한 풀이 (다른 사람 문제 답안)

```Python
def solution(a, b):
    return sum([x*y for x, y in zip(a,b)])
  ```
  
  zip함수를 배운적은 있으나 완벽히 내것으로 소화하고 사용하는덴 힘들었다.  
  
  > zip() : 내장함수로 동일한 개수로 이루어진 자료형을 묶어줌   
  
  예를 들자면 
  
```Python
a = [1,2,3]
b = [a,b,c] 

number_abc = list(zip(a,b))
print(number_abc)
```
  
```
[Output]
[(1,a),(2,b),(3,c)] 
```

같은 인덱스 값을 차례로 들고와 묶어주는 역할을 하는 것이 zip함수이다. 

그래서 여기서 내적 또한 같은 위치의 인덱스를 각 리스트에서 뽑는 것에서 시작한다.  
그래서 for x,y in zip(a,b)를 사용해 뽑은 값들을 x,y로 추출해 곱했고 그 값들을 sum함수를 사용해 더하는 것으로 마무리했다. 


