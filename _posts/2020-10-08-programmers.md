---
layout: post
title: "[Programmers] 프로그래머스 lv2 주식 가격 "
excerpt: "파이썬을 이용한 알고리즘 풀이"
author: Dayeon Lee
date: 2020-10-08 18:30:00 +0800
tags: [python, Programmers, algorithm]
---


## 1. 프로그래머스 주식 가격 문제  
> 초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.   


### 답은 맞췄지만 시간 초과 및 효율성 문제로 실패   

```Python
def solution(prices):
    answer = []
    price = prices.copy()
    for i in price:
        prices.pop(0)
        p = 0
        for j in prices:
            if i <= j:
                p = p + 1
            else : 
                p = 1
                break
        answer.append(p)
    return answer
```


리스트를 copy로 복사해서 사용하는 것은 불필요한 요소로 제거하며 코드를 수정해야하는 것 같다. 
알고리즘을 공부한지 얼마되지 않아 어디서 문제인지는 모르나 성공한 case들의 코드를 보면 
훨씬 단순하게 코드를 짰다는 것을 알 수 있었다. 

2중 for문을 돌리되 리스트 값을 말고 index값으로 순서를 정하는 것이 핵심인 것 같다. 
그래서 https://somjang.tistory.com/entry/Programmers-스택큐-주식가격-Python [솜씨좋은장씨]에서 보고 
코드를 따라 적어보며 이전의 나의 코드들과 비교해보았다.

굳이 쓸 필요가 없는 함수는 제거하고 최대한 단순하고 간단하게 코드를 짜보아야겠다. 
알고리즘은 따로 공부해본적이 없지만 이제부터 하루에 1개라도 풀어봐야겠다. 


### 올바른 코드 예시 
```Python
def solution(prices): 
	answer = [] 
	for i in range(len(prices)): 
		p = 0 
		for j in range(i+1, len(prices)): 
			p = p + 1 
			if prices[i] > prices[j]: 
				break 
		answer.append(p) 
	return answer
  ```

prices의 길이를 이용한 for구문 범위를 지정하고 p라는 값을 0으로 지정해 index값이 증가할 때 
즉, prices의 값이 한 차례씩 이동할 때 만약 이전의 값이 다음의 값보다 크다면 break해 p를 1로 둔다. 
그리고 다음의 값이 이전의 값보다 크거나 같다면 계속해서 1을 추가해주며 answer에 값들을 append해주면 된다. 
생각보다 단순한데 이렇게 간료하게 생각해내는게 아직 쉽지 않은 것 같다.  

앞으로 좋은 코드 예시들을 보며 배워나가야겠다. 
