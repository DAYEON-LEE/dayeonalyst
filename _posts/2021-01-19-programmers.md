---
layout: post
title: "[Programmers] 프로그래머스 lv.2 프린터"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-01-19 21:00:00 +0800
tags: [python, algorithm,pop,stack,queue]
---

> 문제 설명
현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.


1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.


- 조건
  1. 현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.
  2. 인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.
  3. location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며 대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.


|priorities|	location|	return|
|--|--|--|
|[2, 1, 3, 2]	|2	|1|
|[1, 1, 9, 1, 1, 1]	|0|	5|


모든 테스트를 통과한 풀이답안

```Python
def solution(priorities, location):
    loc = [i for i in range(len(priorities))]
    fnl_loc = []
    
    while len(priorities) != 0:
        if priorities[0] == max(priorities):
            fnl_loc.append(loc.pop(0))
            priorities.pop(0)
        else:
            priorities.append(priorities.pop(0))
            loc.append(loc.pop(0))
    print(fnl_loc)
    print(loc)
    return fnl_loc.index(location)+1
```


우선순위 값에서 max값이 첫 번째 위치에 없으면 pop하고 append해 리스트 끝으로 보낸다.   
그리고 중복된 priorities 값이 존재할 수 있으므로 priorities 바뀐 값들의 index를 또한 변경해주어야한다.    

priorities의 값의 index를 loc이라는 이름의 리스트에 넣어 max값이 첫 번째로 나올 때까지 index값의 위치를 변경한다.    

그렇게 반복하다 만약 priorities의 첫 번째값이 max가 나오면 우선순위값이 내림차순일 것이다.   
최종적으로 priorities =  [3,2,1,1]  
           loc [2,3,0,1]

우리가 찾고있는 location=2의 값은 3이었고 현재 3의 위치는 첫 번째에 위치해 return 값은 1이다.    



내가 실패한 코드 
```Python
def solution(priorities, location):
    answer = 0
    fnl_loc = []
    queue = [(i,j) for i,j in enumerate(priorities)]
    while True:
        if queue[0][1] == max(priorities):
            break
        elif queue[0][1] != max(priorities):
            queue.append(queue.pop(0))  
    return [i for i,j in queue].index(location)+1
```

enumerate함수를 사용해 구하는 방식도 가능할 것 같아 시도했지만 time out이라는 결과가 나왔다.    
짐작으로 for구문이 2번 존재하기 때문이 아닐까 생각했다.    
그 부분을 해결하지 못한채 enumerate를 잘 활용한 다른 코드를 발견해 아래에 적어본다. 



배울점이 많은 다른 사람 풀이 코드 
```Python
def solution(priorities, location):
    queue =  [(i,p) for i,p in enumerate(priorities)]
    answer = 0
    while True:
        cur = queue.pop(0)
        if any(cur[1] < q[1] for q in queue):
            queue.append(cur)
        else:
            answer += 1
            if cur[0] == location:
                return answer
```

흥미로웠던 점은 any라는 함수였다.  
처음 보았는데 이렇게 사용할 수 있다는 것을 알게되어 코드를 하나하나 뜯어보기로 하였다.   

dequeue라는 함수를 사용하면 시간복잠도가 더 빠르지만 안쓰고도 코딩을 할 수 있다는 점에 집중해보았다.   
any는 인자중에 참값이 하나라도 있으면 True를 반환하는 함수이다.   

그렇게 첫 번째 값과 두 번째 값을 비교해서 작으면 queue뒤에 append하도록 하였다.  
아니라면 첫 번째 값의 index가 찾고있던 location과 같다면 answer를 return하는 코드였다.  

dequeue함수가 기억이 나지않아 쓰지 못하더라도 이렇게 코드를 쉽고 간결하게 쓸 수 있으면 좋겠다. 
