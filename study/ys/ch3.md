ch. 3 대칭으로 맞추기

동일한 기능이라도 다른 구현 => 코드 스타일을 통일 하자

```python
# 첫 번째 구현: for 루프 사용
result = []
for item in items:
    result.append(process(item))

# 두 번째 구현: map 함수 사용
result = list(map(process, items))

```

코드의 일관성을 유지하여 가독성과 유지보수성

=> 코딩 컨벤션? SQL 컨벤션

