ch. 8 설명하는 변수

표현식 추출
* 코드가 성장하면서 더 커지고 복잡해지는 경향이 있다.
* 이를 이해 후, 일부 표현식을 따로 변수로 추출하고 의도를 잘 나타낼 수 있도로고 명명해주면 좋다.
* 이를 통해 1) 코드의 가독성이 좋아지고, 2) 유지보수가 쉬워진다.

주의할 점
* 협업 관점에서 `코드 정리`와 `동작 변경` 커밋은 명확히 분리하는 것이 좋다.

예시

안좋은 예시
```python
def run_task(task_type, valid_data):
    return (task_type != "backfill" and valid_data == True)
```

좋은 예시
```python
def run_task(task_type, valid_data):
    is_live_task = task_type != "backfill"
    is_valid_data = valid_data == True

    return is_live_task and is_valid_data

```