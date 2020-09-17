---
layout: post
title: "[python] 카카오 API를 이용해 지도의 위도, 경도 알아내기"
excerpt: "카카오 API를 이용해 특정 주소의 위도와 경도를 알아내자."
author: Dayeon Lee
date: 2020-09-17 21:42:00 +0800
tags: [python, Kakao, api, crawling]
---

## 1. 카카오 API key값을 얻기 

### 1-1 카카오 [kakao develper ](https://developers.kakao.com/) 개발자 홈페이지에 접속한다. 

### 1-2 카카오 아이디로 로그인한 후 **내 어플리케이션** 에 들어간다.  

![kakao_api_homepage](https://user-images.githubusercontent.com/56374342/93410774-954f9f80-f8d4-11ea-82ce-5446458f9e3a.PNG)

### 1-3 내 어플리케이션을 추가한 후 들어가면 **카카오api key**들이 주어진다.

![kakao_api_create_application](https://user-images.githubusercontent.com/56374342/93410937-f6777300-f8d4-11ea-95c1-48184dbfd0bd.PNG)

### 1-4 api key들은 네이티브, REST, JAVA, Admin key로 나뉘고 상황에 맞게 사용하면 된다. 

![kakao_api_keys](https://user-images.githubusercontent.com/56374342/93413554-79e79300-f8da-11ea-9d55-233e9a47651b.PNG)



## 2. Rest API를 이용해 카카오맵의 주소 정보에 속하는 JSON파일을 부르기 

필요한 라이브러리만 불러오기 

```Python
import requests
from urllib.parse import urlparse
import pandas as pd
import json
```

url을 요청하기 위해서 requests 라이브러리가 필요하고 불러온 url을 파싱하는 과정에서 urlparse 라이브러리가 필요하다. 
json 파일을 불러오기 위해서 json 라이브러리와 나중에 필요한 데이터만 데이터프레임으로 만들기위해 pandas 라이브러리를 이용한다. 


```Python
for i in address:
    url = 'https://dapi.kakao.com/v2/local/search/address.json?query='+i
    result = requests.get(urlparse(url).geturl(),
                        headers={'Authorization':'KakaoAK **Rest_api_key**'})
    json_obj = result.json()
json_obj
```
여기서 address는 내가 알고 싶은 경도와 위도의 주소를 string형태로 넣어주었다. 
**rest_api_key** 라고 적혀있는 곳에 나의 Rest api키 값을 넣어주면 된다. 


```
  [Output] 
{'documents': [{'address': {'address_name': '경남 창원시 마산회원구 내서읍 삼계리 197-1',
    'b_code': '4812725028',
    'h_code': '4812725000',
    'main_address_no': '197',
    'mountain_yn': 'N',
    'region_1depth_name': '경남',
    'region_2depth_name': '창원시 마산회원구',
    'region_3depth_h_name': '내서읍',
    'region_3depth_name': '내서읍 삼계리',
    'sub_address_no': '1',
    'x': '128.503100300431',
    'y': '35.2260903004507'},
   'address_name': '경남 창원시 마산회원구 내서읍 광려로 8',
   'address_type': 'ROAD_ADDR',
   'road_address': {'address_name': '경남 창원시 마산회원구 내서읍 광려로 8',
    'building_name': '내서운동장',
    'main_building_no': '8',
    'region_1depth_name': '경남',
    'region_2depth_name': '창원시 마산회원구',
    'region_3depth_name': '내서읍 삼계리',
    'road_name': '광려로',
    'sub_building_no': '',
    'underground_yn': 'N',
    'x': '128.503100300431',
    'y': '35.2260903004507',
    'zone_no': '51240'},
   'x': '128.503100300431',
   'y': '35.2260903004507'}],
 'meta': {'is_end': True, 'pageable_count': 1, 'total_count': 1}}
 ```

이 중에 내가 구하고 싶은 값은 x,y값이므로 이렇게 코드를 더해준다. 
