ch. 7 선언과 초기화를 함께 옮기기

타입이 포함된 변수 선언과 초기화 코드가 떨어져 있으면 코드의 가독성이 떨어진다.

단, 파이썬의 경우 별도로 `선언만`하는 문법은 존재하지 않고 동적 타입 언어여서 타입도 따로 명시하지 않는다.

```python
# 변수 선언과 초기화를 동시에 진행
a = 1
b = "hello world"
c = [1, 2, 3]
```

물론 파이썬에서도 비슷한 문제는 생길 수 있다.(변수를 너무 미리 만들어두는 경우)

안좋은 예시
```python
def process_data():
    result = None  # 변수를 선언해놓고...

    # 여러 코드..

    # 한참 뒤에야 초기화
    result = sum(data)
    return result
```

좋은 예시
```python
def process_data():
    
    # 여러 코드..

    result = sum(data)  # 사용할 시점에 바로 선언 + 초기화
    return result
```