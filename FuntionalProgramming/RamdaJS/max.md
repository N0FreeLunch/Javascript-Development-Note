## max
> Returns the larger of its two arguments.
- 두 인자를 받아 더 큰 값을 반환한다.

> See also maxBy, min.

## 표현
```
Ord a => a → a → a
```
- `Ord a =>` 순서가 있는 타입의 값을 a라고 한다는 의미이다.
- `a →` 첫 번째 인자로 순서가 있는 값을 받는다.
- `→ a →` 두 번째 인자로 첫 번째 인자와 순서를 비교할 수 있는 값을 받는다.
- `→ a` 인자로 받은 두 수 중에서 순서가 큰 쪽의 인자를 반환한다.

## 예제
```
R.max(789, 123); //=> 789
R.max('a', 'b'); //=> 'b'
```
- `R.max(789, 123)` `123`보다 `789`가 더 크다.
- `R.max('a', 'b')` `'a'`보다 `'b'`가 크다

## Reference
- https://ramdajs.com/docs/#max
