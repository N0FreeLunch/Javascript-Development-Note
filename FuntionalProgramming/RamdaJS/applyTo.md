## applyTo
> Takes a value and applies a function to it.
- 받은 값을 함수에 적용한다.
> This function is also known as the thrush combinator.
- 이 함수는 (왼쪽의 함수 부터 값을 할당하여 그 결과 값을 오른쪽의 다음 함수에 할당하는 방식으로 전개하는) thrush combinator로 알려져 있다.

### 설명
- 첫 번째 인자로 값을 받고
- 두 번째 인자로 평가되지 않은 함수를 받으면
- 첫 번째 인자로 받은 값을 두 번째 인자로 받은 함수의 인자로 넣어 평가한 값을 반환한다.

### 문법
```
R.applyTo(x, f): *
```
- `x`: The value
- `f`: The function to apply
- Returns * The result of applying `f` to `x`

### 표현
```
a → (a → b) → b
```
- `a →`: 첫 번째 인자로 임의의 종류(a)에 해당하는 값을 받는다.
- `(a → b)`: 두 번째 인자로 첫 번째 인자의 종류와 일치하는 인자를 받는 함수를 받는다. 두 번째 인자의 함수에 첫 번째 인자로 받은 값을 넣어 (이 때 종류가 일치) 평가된 결과 값을 얻는다.
- `→ b`: 결과 값의 타입은 두 번째 인자로 받은 함수의 결과 값이므로 `(a → b)`의 결과 타입인 b가 된다.

### 예제
```js
const t42 = R.applyTo(42);
t42(R.identity); //=> 42
t42(R.add(1)); //=> 43
```
- `R.applyTo(42)` 는 인자로 들어 온 42 값을 다음으로 받는 함수의 인자 할당하기 위한 함수를 만든다. 그 함수가 `t42`
- `t42(R.add(1));` 42란 값을 인자로 할당하는 함수 `t42`에 `R.add(1)`을 인자로 할당하였다.
- 따라서`t42(R.add(1));`의 결과는 `R.add(1)(42)` 라서 43

## References
- https://ramdajs.com/docs/#applyTo
- https://github.com/ramda/ramda/blob/master/test/applyTo.js
- https://github.com/ramda/types/blob/develop/types/applyTo.d.ts
