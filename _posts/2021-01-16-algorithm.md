---
layout: post
title: "[Algorithm] 알고리즘 우선순위 큐와 힙 그리고 스택 "
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-01-16 17:35:00 +0800
tags: [python, algorithm, heap, queue, stack]
---


## 1. 힙(Heap) 

> 힙 :  리스트에서 가장 작은(또는 가장 큰) 요소에 반복적으로 접근하는 프로그램에 유용 


- 힙의 시간복잡도
  1. 가장 작은 요소를 처리하는 시간복잡도는 O(1)
  2. 그 외의 조회, 추가, 수정을 처리하는 시간복잡도는 O(log n)
  
 
## 2. 스택(Stack) 

> 스택 : 배열 인덱스 접근이 제한되며, 후입선출 (Last In, First Out)구조 

- 스택의 시간복잡도
  1. 모든 스택의 시간복잡도는 O(1)

- 함수
  1. push : 스택 맨 끝에 항목을 삽입
  2. pop : 스택 맨 끝 항목을 반환하는 동시에 제거 
  3. top/peek : 스택 맨 끝 항목을 조회
  4. empth : 스택이 비어있는지 확인
  5. size : 스택 크기를 확인 
  

```Python
class Stack(object):
  def __init__(self):
    self.items = []
  
  def isEmpth(self):
    return not bool(self.item)
   
   def push(self,value):
    self.items.append(value)
   
   def pop(self):
    value = self.items.pop()
    if value is not None:
      return value
    else:
      print('Stack is empty.)
      
   def size(self):
    if self.items:
      return len(self.items)
   
   def peek(self):
    if self.items:
      return self.items[-1]
    else:
      print('Stack is empty.')
    
    def __repr__(self):
      return repr(self.items)
      
 if __name__ = '__main__':
  stack = Stack()
  print('스택이 비었나요? {0}'.format(stack.isEmpty()))
  print('스택에 숫자 0~9를 추가합니다.')
  for i in range(10):
    stack.push(i)
  print('스택 크기:{0}'.format(stack.size()))
  print('peek:{0}'.format(stack.peek()))
  print('pop:{0}'.format(stack.pop()))
  print('peek:{0}'.format(stack.peek()))
  print('스택이 비었나요? {0}'.format(stack.isEmpty()))
  pritn(stack)
```


## 3. 큐(Queue)

> 큐 : 먼저 들어온 데이터가 먼저 나가는 선입선출(First In, First Out)구조  

- 시간복잡도
  1. 모든 시간복잡도는 O(1)
  
 - 함수 
  1. enqueue : 큐 뒤쪽에 항목을 삽입
  2. dequeue : 큐 앞쪽에 항목을 반환하고 제거 
  3. peek/fornt : 큐 앞쪽의 항목을 조회
  4. empty : 큐가 비어있는지 확인
  5. size : 큐의 크기를 확인 
  
```Python
class Queue(self):
  def __init__(self):
    return self.items = []
  
  def isEmpty(self):
    return not bool(self.items)
  
  def enqueue(self):
    self.items.insert(0,item)
    
  def dequeue(self):
    value = self.items.pop()
    if value is not None:
      return value
    else:
      print('Queue is empty.')
    
  def size(self):
    return len(self.items)
    
  def peek(self):
    if self.items:
      return self.items[-1]
    else:
      print('Queue is empty.')
      
  def __repr__(self):
    return repr('Queue is empty.')
    
if __name__ == '__main__':
  queue = Queue()
  print('큐가 비었나요? {0}'.format(queue.isEmpty()))
  print('큐에 숫자 0~9를 추가합니다.')
  for i in range(10):
    queue.enqueue(i)
  print('큐 크기: {0}'.format(queue.size()))
  print('peek :{0}'.format(queue.peek()))
  print('dequeue': {0}'.format(queue.dequeue()))
  print('peek: {0}'.format(queue.peek()))
  print('큐가 비었나요? {0}'.format(queue.isEmpty()))
  print(queue)
```
