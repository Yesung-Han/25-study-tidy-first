ch. 1 보호 구문

보호 구문의 핵심 아이디어는 함수의 진입점에서 유효하지 않은 조건들을 먼저 걸러내는 것이다.

* 중첩된 if 문이 줄어들어서 가독성이 향상된다.
* 함수의 핵심 로직이 더 명확하게 보인다.
* 전제 조건들이 코드 시작 부분에 모여있어서 이해하기 쉽다.

ex)

```python
# 중첩된 조건문을 사용한 방식
def process_order(order, user):
    if user.is_authenticated:
        if user.has_sufficient_balance:
            if order.is_valid:
                # 주문 처리 로직
                order.process()
                user.deduct_balance(order.amount)
                return "주문이 성공적으로 처리되었습니다"
    return "주문 처리에 실패했습니다"

# 보호 구문을 사용한 방식
def process_order(order, user):
    # 전제 조건들을 먼저 검사
    if not user.is_authenticated:
        return "인증되지 않은 사용자입니다"
    
    if not user.has_sufficient_balance:
        return "잔액이 부족합니다"
        
    if not order.is_valid:
        return "유효하지 않은 주문입니다"
    
    # 핵심 비즈니스 로직
    order.process()
    user.deduct_balance(order.amount)
    return "주문이 성공적으로 처리되었습니다"
```

두번째 방식의 장점

* 각 조건이 독립적으로 검사되어 로직이 명확하다.
* 오류 상황에 대한 처리가 명시적이고 구체적이다.
* 성공 경로가 더 명확하게 보인다.
* 중첩된 if문이 존재하지 않아 가독성이 더 좋다.
 
하지만 다음과 같은 경우 무조건 부정구문인 not in을 적용하기보다 [커밋](https://github.com/Bogdanp/dramatiq/pull/470/files)을 참고해보자

```python
if (조건):
    ... 코드 ...
... 다른 코드 ...
```


### 업무 적용 사례

```python
def get_impala_connection(
    app_name: str = "",
    phase: str = "",
    branch: str = "",
    target_idc: str = "",
) -> Impala:
    """Impala 연결 객체를 생성하는 함수

    Args:
        app_name (str, optional): 애플리케이션 이름. Defaults to "".
        phase (str, optional): 환경 설정. Defaults to "".
        branch (str, optional): 브랜치 이름. Defaults to "".
        target_idc (str, optional): 대상 IDC. Defaults to "".

    Returns:
        Impala: Impala 연결 객체

    Raises:
        ValueError: target_idc가 'dc1' 또는 'dc2'가 아닌 경우
    """
    if target_idc not in ["dc1", "dc2"]:
        raise ValueError("target_idc must be 'dc1' or 'dc2'")

    config_path = (
        "db_config.dc1"
        if target_idc == "dc1"
        else "db_config.dc2"
    )

    config = CloudConfig(app_name=app_name, phase=phase, branch=branch).get(config_path)
    return Impala(**config.get(""))
```