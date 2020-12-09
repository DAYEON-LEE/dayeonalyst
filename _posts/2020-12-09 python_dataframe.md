---
layout: post
title: "[python] 중복된 행 조회/삭제, 특정값 대체, 특정값을 포함한 행만 추출"
excerpt: "DataFrame에서 duplicated(), drop_duplicates(), replace(), appplymap(), map(), mapapply()등의 함수를 이용해보자."
author: Dayeon Lee
date: 2020-12-09 19:00:00 +0800
tags: [python, drop_duplicates, replace, apply, map, applymap, duplicated]
---

## 중복된 행 조회 및 삭제 
### 1. duplicated, drop_duplicates 함수 

|name|age|blood|
|--|--|--|
|정국|24|A|
|진|28|B|
|태형|26|O|
|정국|24|A|
|남준|26|AB|


이런 데이터가 주어진다고 하자. 

