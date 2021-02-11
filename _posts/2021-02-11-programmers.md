---
layout: post
title: "[MYSQL] 오랜 기간 보호한 동물(1)"
excerpt: "MYSQL을 이용한 알고리즘 공부"
author: Dayeon Lee
date: 2021-02-10 13:40:00 +0800
tags: [SQL,MYSQLL,programmers,left join,where,limit,isnull]
---

문제

> 아직 입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일 순으로 조회해야 합니다.

|**NAME**|	**TYPE**|	**NULLABLE**|
|--|--|--|
|ANIMAL_ID	|VARCHAR(N)|	FALSE|
|ANIMAL_TYPE|	VARCHAR(N)	|FALSE|
|DATETIME	|DATETIME	|FALSE|
|INTAKE_CONDITION|	VARCHAR(N)	|FALSE|
|NAME	|VARCHAR(N)	|TRUE|
|SEX_UPON_INTAKE|	VARCHAR(N)	|FALSE|

이때 결과는 아이디 순으로 조회해주세요. 예를 들어 ANIMAL_INS 테이블이 다음과 같다면

|ANIMAL_ID	|ANIMAL_TYPE	|DATETIME	|INTAKE_CONDITION	|NAME	|SEX_UPON_INTAKE|
|--|--|--|--|--|--|
|A350276|	Cat|	2017-08-13 13:50:00	|Normal	|Jewel	|Spayed Female|
|A381217	|Dog	|2017-07-08 09:41:00	|Sick|	Cherokee	|Neutered Male|

예를 들어 ANIMAL_OUTS 테이블이 다음과 같다면

|ANIMAL_ID	|ANIMAL_TYPE|	DATETIME|	NAME	|SEX_UPON_OUTCOME|
|--|--|--|--|--|
|A349733|	Dog	|2017-09-27 19:09:00	|Allie|	Spayed Female|
|A352713|	Cat	|2017-04-25 12:25:00|	Gia	|Spayed Female|
|A349990	|Cat|	2018-02-02 14:18:00	|Spice	|Spayed Female|

SQL문을 실행하면 다음과 같이 나와야 합니다.

|NAME|	DATETIME|
|--|--|
|Shelly|	2015-01-29 15:01:00|
|Jackie|	2016-01-03 16:25:00|
|Benji	|2016-04-19 13:28:00|

```SQL
SELECT ANIMAL_INS.NAME, ANIMAL_INS.DATETIME 
FROM ANIMAL_INS LEFT JOIN ANIMAL_OUTS
ON ANIMAL_INS.ANIMAL_ID = ANIMAL_OUTS.ANIMAL_ID
WHERE ANIMAL_OUTS.ANIMAL_ID IS NULL
ORDER BY ANIMAL_INS.DATETIME LIMIT 3;
```
left join하면 ANIMAL_INS에 존재하고 ANIMAL_OUTS에 존재하지 않는 ANIMAL_ID는 NULL값으로 표시가 된다.  
그럼 그 데이터셋에서 WHERE를 사용해 조건을 걸어주고 ORDER BY로 DATETIME정렬후 상위 3개만 보여준다.  
그것을 하는 함수가 LIMIT이다.   
