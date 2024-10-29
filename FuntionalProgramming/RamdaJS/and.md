## and

> Returns the first argument if it is falsy, otherwise the second argument.
- 첫 번째 거짓이라면 첫 번째 인자를 반환하고 첫 번째 인자가 참이라면 두 번째 인자를 반환한다.

> Acts as the boolean and statement if both inputs are Booleans.
- 만약 입력된 두 인자가 불리언 타입이면 불리언 and 연산자 처럼 동작한다.

> See also [both](./both.md), [or](./or.md).

### 설명

- 두 인자를 받아서 첫 번째 인자를 불리언 타입으로 형변환 한 값이 참이면 첫 번째 인자를 반환하고, 첫 번째 인자의 불리언 형변환 값이 거짓이면 두 번째 인자의 불리언 형변환 값이 참일 때 두 번째 값을 반환하고 그렇지 않으면 거짓을 반환한다.
- 논리학의 논리 연산으로 사용되는 and가 참인지 거짓인지를 판별하는 것에 반해, 프로그래밍 언어에서 `&&` 연산자는 앞의 값이 truely이면 앞의 값을 반환하고, 앞의 값이 falsy이고 뒤의 값이 truely 이면 뒤의 값을 반환한다. Ramda의 and 함수도 논리학의 논리 연산과 달리 프로그래밍 언어의 `&&`의 방식으로 동작한다.

### 문법

```
R.and(a, b): Any
```

### 표현
```
a → b → a | b
```
- `a →`: 인자 a를 받고
- `b →`: 인자 b를 받아서
- `→ a | b`: a 또는 b 인자를 반환한다.

## 예제
```js
R.and(true, true); //=> true
R.and(true, false); //=> false
R.and(false, true); //=> false
R.and(false, false); //=> false
```
- 위 예제를 보면 실제 불리언 연산에서의 and 연산자와 정의는 다르지만 2개의 인자를 불리언 타입으로 받을 경우 동일한 결과를 만드는 것을 알 수 있다.

## References
- https://ramdajs.com/docs/#and
- https://github.com/ramda/ramda/blob/master/test/and.js
- https://github.com/ramda/types/blob/develop/types/and.d.ts
