
ch. 1 보호 구문

- 전제 조건이 명시적으로 드러날때 보호구문이 있는 코드를 적용하자
- 보호구문을 남용하면 안된다. 읽기가 가다로울 수 있다. 7~8개의 보호구문

[as-is]
```
if (조건)
	if (다른 조건 부정)
	... 코드 ... 
```

[to-be]
```
if (조건 부정) return
if (다른 조건) return
	... 코드 ... 
```



[example]
```python
def post(self, request, *args, **kwargs):  
    if not request.user.is_authenticated:  
        return HttpResponse('Unauthorized', status=status.HTTP_401_UNAUTHORIZED)  
  
    if not self.has_permission(request.user, f'change_{self.target_model._meta.model_name}'):  
        return Response({"error": "Permission denied"}, status=status.HTTP_403_FORBIDDEN)


.
.
.

```