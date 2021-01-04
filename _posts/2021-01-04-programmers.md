---
layout: post
title: "[Programmers] 프로그래머스 lv1 시저암호 "
excerpt: "파이썬을 이용한 알고리즘 풀이"
author: Dayeon Lee
date: 2020-01-04 22:35:00 +0800
tags: [python, Programmers, algorithm]
---


## 1. 프로그래머스 시저암호 문제  
> 어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 AB는 1만큼 밀면 BC가 되고, 3만큼 밀면 DE가 됩니다. z는 1만큼 밀면 a가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

**조건**
1. 공백은 아무도 밀어도 공백입니다.
2. s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
3. s의 길이는 8000이하입니다.
4. n은 1이상, 25이하인 자연수입니다. 


|s|n|result|
|--|--|--|
|["AB"]|1|"BC"|
|["Z"|1|"a"|
|["a B z"]|4|"e F d"|


### 모든 테스트를 통과한 풀이답안

```Python
def solution(s, n):
    answer = ''
    for i in s:
        if i.isupper():
            answer = answer + chr((ord(i)-ord('A')+n)%26+ord('A'))
        elif i.islower():
            answer = answer + chr((ord(i)-ord('a')+n)%26+ord('a'))
        else:
            answer = answer + ' '
    return answer
  ```

**answer = answer + chr((ord(i)-ord('A')+n)%26+ord('A'))** 이 부분의 코드를 생각해내는게 어려웠습니다.   

우선 아스키코드 변환하는 함수를 소개하겠습니다.   

> ord() : 특정한 한 문자를 아스키코드값으로 변환해주는 함수  
> chr() : 아스키코드값 즉, 특정한 숫자를 문자로 변환해주는 함수


 예를 들면 대문자 A는 아스키코드값이 65 특정한 숫자에 할당된 것을 말한다.   
 
* 여기서 포인트는 식을 세우는 것과 chr, ord함수를 알고있느냐인 것 같습니다. 
