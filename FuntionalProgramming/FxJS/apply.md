## apply
```
(f, iterable) => f(...iterable)
```
- 함수에 iterable을 넣는 함수

```
const args = [10, 20];
add(...args); // 30
apply(add, args); // 30
apply(add)(args); // 30
```
