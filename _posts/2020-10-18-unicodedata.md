---
layout: post
title: "[python] Unicodedata 라이브러리를 이용해 구두점 문자 제거 "
excerpt: "unicodedata를 이용해 텍스트마이닝을 해보자."
author: Dayeon Lee
date: 2020-10-18 23:30:00 +0800
tags: [python, text_mining, unicodedata]
---


# 구두점 삭제 

```Python
# 구두점 삭제 
import unicodedata
import sys

# 텍스트를 만듬
text_data = ['Hi!!!! I. Love. This. Song....',
            '10000% Agree!!!! #LoveIT',
            'Right?!?!?!']
# 구두점 문자로 이룯어진 딕셔너리 생성
punctuation = dict.fromkeys(i for i in range(sys.maxunicode) if unicodedata.category(chr(i)).startswith('P'))
# 문자열의 구두점을 삭제 
[string.translate(punctuation) for string in text_data]
```

```
[Output] ['Hi I Love This Song', '10000 Agree LoveIT', 'Right']
```

translate는 속도가 매우 빠른 함수로 유용하게 사용할 수 있는 인기 많은 함수입니다.  

유니코드 구두점을 키로 하고 값은 None인 딕셔너리를 생성 후에 모든 Punctuation에 있는 모든 문자를 None으로 바꾸어 구두점을 삭제합니다. 

