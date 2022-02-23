## and
- `R.and()`

## 설명
```
R.and(boolean, boolean)
```
- 두 인자를 받아서 두 인자의 불리언 and 연산 결과를 반환

## 표현
```
a → b → a & b
```
- `a →` 인자 a를 받고
- `b →` 인자 b를 받아서
- `→ a & b` a와 b의 and 연산을 반환
- 도큐먼트에 `a & b`가 아니라 `a | b`으로 되어 있는데 이상하다.

## 예제
```
R.and(true, true); //=> true
R.and(true, false); //=> false
R.and(false, true); //=> false
R.and(false, false); //=> false
```

## Reference
- https://ramdajs.com/docs/#and
