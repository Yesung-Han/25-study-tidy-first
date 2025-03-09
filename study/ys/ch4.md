ch. 4 새로운 인터페이스로 기존 루틴 부르기



pass-through interface : 복잡한 기존 인터페이스를 그저 호출만 하는 인터페이스

=> 레거시 코드 고칠때 유용할 듯

복잡한 기존 인터페이스 에서 쓰는 기능만 pass-through interface 로 제공하고, 제공하는 부분을 하나씩 바꿔 나감

[as-is]
```python
class ComplexSystem:
    def perform_operation(self, data, flag, timeout, retries):
        # 복잡한 로직
        pass

# 기존 방식으로 호출
system = ComplexSystem()
system.perform_operation(data, True, 30, 3)

```


[to-be]
```python
class SimpleInterface:
    def __init__(self):
        self.system = ComplexSystem()

    def simple_operation(self, data):
        # 통로 인터페이스를 통해 간단하게 호출
        self.system.perform_operation(data, True, 30, 3)

# 새로운 인터페이스를 통해 호출
interface = SimpleInterface()
interface.simple_operation(data)
```


pass-through interface 와 같이 레거시 코드 변경이 쉬워지는 다른 기법들

1. 거꾸로 코딩하기 (Reverse Engineering 또는 Backward Coding)

```python
def legacy_function(data):
	result = []
	for item in data:
		if item % 2 == 0:
			result.append(item * 2)
	return result
```
=> 짝수에 *2를 해서  추출하는 기능이구나


```python
def modern_function(data):
	return [item * 2 for item in data if item % 2 == 0]
```


1. 테스트 우선 코딩 (Test-First Development 또는 Test-Driven Development, TDD)

	_TDD의 일반적인 사이클:_
	
	1. 실패하는 테스트 작성​
	2. 테스트를 통과하는 최소한의 코드 작성​
	3. 코드 리팩토링

```python
def test_add(): assert add(2, 3) == 5
```


```python
def add(a, b): return a + b
```


1. 도우미 설계 (Helper Design)
- 복잡한 코드나 중복되는 로직을 별도의 함수나 클래스로 분리하여 코드의 재사용성과 가독성을 높이는 방법
[as-is]
```python
def process_data(data):
    # 데이터 전처리
    data = [item.strip().lower() for item in data]
    # 데이터 필터링
    data = [item for item in data if len(item) > 3]
    return data
```

[to-be]
```python
def preprocess_item(item):
    return item.strip().lower()

def filter_item(item):
    return len(item) > 3

def process_data(data):
    data = [preprocess_item(item) for item in data]
    data = [item for item in data if filter_item(item)]
    return data
```