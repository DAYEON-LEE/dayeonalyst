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
처음엔 문제를 잘 못 이해해서 앞에 한글자라도 같으면 True라고 생각해 코딩을 했다.   
그래서 엉뚱한 접근으로 다시 접근하고 시도하다가 결국 다른 사람의 코드를 참고하기로 했다.   


모든 테스트 통과 코드 (n차 시도)    
```Python
def solution(phoneBook):
    phoneBook = sorted(phoneBook)

    for p1, p2 in zip(phoneBook, phoneBook[1:]):
        print(p1,p2)
        if p2.startswith(p1):
            return False
    return True
```
와..zip을 활용하고 싶었는데 어떻게 써야할지 몰라서 못썼는데 이렇게 쓸 수도 있구나를 배웠다.  
그리고 여기서 전화번호가 string으로 문자열이라 정렬을 하고 옆으로만 비교하면 되는 문제였다.   

전에도 string이라 그렇게 접근하는 법을 익혔는데도 반복학습의 부재라고 생각한다.
복습을 계속 하면서 더 나은 코드에 익숙해져야겠다.   


해쉬를 이용한 정석 풀이 코드 
```Python
def solution(phone_book):
    answer = True
    hash_map = {}
    for phone_number in phone_book:
        hash_map[phone_number] = 1
    for phone_number in phone_book:
        temp = ""
        for number in phone_number:
            temp += number
            if temp in hash_map and temp != phone_number:
                answer = False
    return answer
```

해시에 대한 개념을 더 명확히 공부하기 위해 들고온 코드이다.  
딕셔너리를 사용하면서 문제를 완벽하게 캐치한 코드라고 생각한다.   

전화번호를 하나씩 추가하면서 그 값이 hash_map에 자신의 값을 제외하고 포함되는지의 여부로 True, False로 나누었다.   
