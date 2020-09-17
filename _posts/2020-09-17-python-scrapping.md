---
layout: post
title: "[python] 카카오 API로 카카오맵 JSON파일 불러오기"
excerpt: "카카오 API를 이용해 카카오맵의 정보를 이용하자."
author: Dayeon Lee
date: 2020-09-17 21:42:00 +0800
tags: [python, Kakao, api, crawling]
---

## 1. 카카오 API key값을 얻기 

### 1-1 카카오 [kakao develper ](https://developers.kakao.com/) 개발자 홈페이지에 접속한다. 

### 1-2 카카오 아이디로 로그인한 후 **내 어플리케이션** 에 들어간다.  

![kakao_api_homepage](https://user-images.githubusercontent.com/56374342/93410774-954f9f80-f8d4-11ea-82ce-5446458f9e3a.PNG)

### 1-3 내 어플리케이션을 추가한 후 들어가면 카카오api key들이 주어진다.

![kakao_api_create_application](https://user-images.githubusercontent.com/56374342/93410937-f6777300-f8d4-11ea-95c1-48184dbfd0bd.PNG)

### 1-4 api key들은 네이티브, REST, JAVA, Admin key로 나뉘고 상황에 맞게 사용하면 된다. 

![kakao_api_keys](https://user-images.githubusercontent.com/56374342/93411129-6ab21680-f8d5-11ea-8100-b08e614deee6.PNG)

