---
layout: post
title: "[Programmers] 프로그래머스 lv.2 뉴스 클러스터링"
excerpt: "파이썬을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-23 13:00:00 +0800
tags: [python, algorithm,programmers]
---
 
 
테스트 통과한 코드 
```Python
def solution(str1, str2):
	list_str1 =[]
	list_str2 =[]

	for s1, slice_s1 in zip(str1, str1[1:]) : 
		join_str = "".join([s1,slice_s1])
		if join_str.isalpha() :
			list_str1.append( join_str.lower() )
	print(list_str1)
    
	for s2, slice_s2 in zip(str2, str2[1:]) :  
		join_str = "".join([s2,slice_s2])
		if join_str.isalpha() :
			list_str2.append(join_str.lower())
			
	if len(list_str1) > len(list_str2) : 
		inter =  [list_str1.remove(x) for x in list_str2 if x in list_str1] 
	else :
		inter = [list_str2.remove(x) for x in list_str1 if x in list_str2] 
        
	list_uni = list_str1 + list_str2
	uni = len(list_uni)
	
	if uni ==0 :
		return 65536
    print(len(inter))
	return int(len(inter)/uni * 65536 )
```

isalpha()로 문자만 true를 반환하는 함수로 특수문자나 숫자가 들어간 값은 제외시켰다.   
그리고 모두 대문자, 소문자 구별을 없애기 위해 소문자로 변경해주어 list에 각각 넣고 각각 교집합과 합집합을 구했다. 

리스트 길이가 짧은 값이 리스트 긴 값의 값들에 포함된 것만이 교집합일 것이고 전체값에서 교집합값만이 제거된 것이 합집합일 것이다. 
그런 원리로 알고리즘을 작성하였다. 


다른 사람 풀이 
```Python
import re
import math

def solution(str1, str2):
    str1 = [str1[i:i+2].lower() for i in range(0, len(str1)-1) if not re.findall('[^a-zA-Z]+', str1[i:i+2])]
    str2 = [str2[i:i+2].lower() for i in range(0, len(str2)-1) if not re.findall('[^a-zA-Z]+', str2[i:i+2])]

    gyo = set(str1) & set(str2)
    hap = set(str1) | set(str2)

    if len(hap) == 0 :
        return 65536

    gyo_sum = sum([min(str1.count(gg), str2.count(gg)) for gg in gyo])
    hap_sum = sum([max(str1.count(hh), str2.count(hh)) for hh in hap])

    return math.floor((gyo_sum/hap_sum)*65536)
```
if 문과 정규표현식을 이렇게 사용할 수 있다는 예시였다. list comprehension을 너무나도...잘 이용한 케이스..
set으로 교집합과 합집합을 구해서 요소의 개수를 세어서 길이를 구해 풀었다.   

