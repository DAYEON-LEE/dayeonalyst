---
layout: post
title: "[python] folium 지도 시각화"
excerpt: "folium으로 지도(map)시각화를 "
author: Dayeon Lee
date: 2020-09-11 21:42:00 +0800
tags: [python, folium]
---

## folium 지도 시각화
### 1. 필요한 라이브러리 
우선 지도 시각화에 필요한 라이브러리를 불러오는 작업이 필요하다. 
```python 
import json
import folium
import pandas as pd
```
### 2. 시각화에 필요한 데이터 프레임
```python
df = pd.DataFrame({'index':['창원시의창구','창원시성산구','창원시진해구','창원시마산합포구','창원시마산회원구'],
                  'count':[30,20,50,10,90]})
df
```
라이브러리 folium으로 창원시 구의 count에 따른 지도 시각화를 할 예정이다.
```
	[Output]
        index        count   \
    0  창원시의창구     30  
    1  창원시성산구     20  
    2  창원시진해구     50  
    3  창원시마산합포구  10    
    4  창원시마산회원구  90 
```
### 3. 지도의 정보가 들어가있는 json파일 
시각화를 하기위해서는 json파일이 필요한데 나는 여기 올라와있는 깃헙의 파일을 다운받아 사용했다.
> json 깃헙에서 제공 : [json파일](https://github.com/DAYEON-LEE/southkorea-maps/tree/master/kostat/2013/json) 
> 
하지만 창원시의 데이터만을 들고와 편집했다. 
```
	[Output]
{'type': 'FeatureCollection',
 'features': [{'type': 'Feature',
   'properties': {'code': '38115',
    'name': '창원시진해구',
    'name_eng': 'Jinhaegu',
    'base_year': '2013'},
   'geometry': {'type': 'Polygon',
    'coordinates': [[[128.74342173830925, 35.163933102810184],
    .
    .
    .
    }
  ```
  다음과 같이 type안에 features안에 properties안에 name이 창원시만을 포함하고 있다. 
  ### 4. folium으로 지도 시각화 
  ```python
  map = folium.Map(location=[35.2258,128.6075],zoom_start=9,
                 tiles='Stamen Toner')
map.choropleth(geo_data = geo_str,
               data = df,
               columns = ('index','count'),
               fill_color = 'PuRd',
               key_on = 'feature.properties.name')
map  
```
- location :  창원시의 위도, 경도
- zoom_start : 얼마나 확대할지 사이즈
- tiles : map의 디자인 종류
- fill_color : 지도의 색을 칠할 색상칼러
- key_on : json파일에서 지역명이나 이름이 포함되어있는 위치



![png](dayeonlyst.github.io/images/folium_map_changwon_ex.PNG)



이렇게 folium으로 지도 시각화를 진행해보았다. 



