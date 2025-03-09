ch. 5 읽는 순서


코드를 읽기 좋은 순서대로 정렬 하자

완벽한 순서는 없다.


ex?) import 순서 ?
```python
# 표준 라이브러리 모듈
import os
import sys

# 서드 파티 모듈
import requests
import numpy as np

# 로컬 모듈
from my_project import my_module

```

ex) 상위 수준에서 하위 수준으로 구성
```python
def main():
    data = load_data()
    processed_data = process_data(data)
    save_data(processed_data)

def load_data():
    # 데이터 로드 로직
    pass

def process_data(data):
    # 데이터 처리 로직
    pass

def save_data(data):
    # 데이터 저장 로직
    pass

```

ex) 관련된 코드를 인접한 곳에 배치
```python
class DataProcessor:
    def __init__(self, data):
        self.data = data

    def clean_data(self):
        # 데이터 정제 로직
        pass

    def analyze_data(self):
        # 데이터 분석 로직
        pass

    def report_data(self):
        # 데이터 보고서 생성 로직
        pass

```


