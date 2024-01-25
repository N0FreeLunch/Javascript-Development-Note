## or
> Returns the first argument if it is truthy, otherwise the second argument. Acts as the boolean or statement if both inputs are Booleans.
- 첫 번째 인자가 truthy 이면 첫 번째 인자를 반환하고, 그렇지 않으면 두 번째 인자를 반환한다. 만약 입력된 두 값이 불리언 타입의 값이면 불리언 or 구문 처럼 행동한다.

> See also either, and.

### 설명
- 인자로 받은 두 값 중에서 하나의 값만 반환한다. 이 때 반환의 기준은 첫 번째 인자로 받은 값이 truthy에 해당하는 값인지 falsy에 해당하는 값인지에 따라 다르다.
- 첫 번째 인자가 truthy에 해당하면 첫 번째 인자를 반환하고, 첫 번째 인자가 falsy에 해당하면 두 번째 인자를 반환한다.
- 예를 들어 '값A'가 존재할 때는 '값A'를 사용하고 '값A'가 없으면 디폴트로 '값B'를 대신 사용하려는 코드를 함수형 코드로 사용하고자 할 때 생각해 볼 수 있는 방식이다.

### 표현
```
a → b → a | b
```
- `a →` 임의의 첫 번째 인자를 받고
- `→ b →` 임의의 두 번째 인자를 받는다.
- `→ a | b` 첫 번째 인자 또는 두 번째 인자를 반환한다.

### 예제
```js
R.or(true, true); //=> true
R.or(true, false); //=> true
R.or(false, true); //=> true
R.or(false, false); //=> false
```
- `R.or(true, true)` 첫 번째 인자가 truthy에 해당하므로 이므로 첫 번째 인자를 반환한다.
- `R.or(true, false)` 첫 번째 인자가 truthy에 해당하므로 이므로 첫 번째 인자를 반환한다.
- `R.or(false, true)` 첫 번째 인자가 falsy에 해당하므로 두 번째 인자를 반환한다.
- `R.or(false, false)` 첫 번째 인자가 falsy에 해당하므로 두 번째 인자를 반환한다.

## Reference
- https://ramdajs.com/docs/#or
