## unless
> Tests the final argument by passing it to the given predicate function.
- 마지막 인자가 주어진 술어함수를 통과하는지를 테스트한다.
> If the predicate is not satisfied, the function will return the result of calling the whenFalseFn function with the same argument.
- 술어함수를 만족하지 못한다면, unless 함수는 실패했을 때 실행하는 함수(whenFalseFn)를 동일한 인자를 전달하여 호출한 결과를 반환한다.
> If the predicate is satisfied, the argument is returned as is.
- 만약 술어 함수를 만족하면, 인자는 그대로 반환된다.

> See also ifElse, when, cond.

### 설명
- 어떤 값이 특정한 조건을 만족할 때 원본 그대로의 값을 반환하고, 그렇지 않은 경우 특수한 변환을 거친 값을 얻는다.
- 첫 번째 인자로 조건을 만족하는지 확인하는 술어함수를 받고, 두 번째 인자로 특수한 변환을 위한 함수를 받으며, 세 번째 인자로 어떤 값을 받는다.
- 어떤 값을 변환하고 싶은데 특정 조건을 만족하지 못하면 변환하지 않는다는 의미로도 사용할 수 있다.
- 세 번째 인자로 받은 값이 첫 번째 인자의 함수의 인자로 전달되었을 때, 참이라면 세 번째 인자값을 그대로 반환하고, 거짓이라면 두 번째 인자에 세 번째 인자값을 전달한 결과값을 얻는다.

### 표현
```
(a → Boolean) → (a → b) → a → a | b
```
- `(a → Boolean) →`: 첫 번째 인자로 술어 함수를 받는다. 이 술어함수는 인수로 세 번째 인자의 값을 받으므로 `a` 타입 파라메터를 갖는다.
- `→ (a → b) →`: 두 번째 인자로 첫 번째 인자로 받은 술어함수의 평가 결과가 거짓일 때 최종 반환할 값을 결정하기 위한 함수를 받는다. 세 번째 인자로 받은 값을 전달 받으므로 `a` 타입 파라메터를 갖는다.
- `→ a →`: 세 번째 인자로 첫 번째 인자로 받은 함수의 인자로 전달할 값을 받는다. 이 값을 첫 번째 인자로 받은 함수에 전달 했을 때, 함수가 반환하는 참 거짓의 결과에 따라 거짓이면 두 번째 인자로 받는 함수의 인자로 값을 전달한다.
- `→ a | b`: 최종 반환 값은 세 번째로 받은 인자가 술어함수를 만족했을 때는 세 번째 인자 그대로의 값을 반환하므로 `a` 타입 파라메터를 가지며, 술어함수를 만족하지 못했을 때는 두 번째 인자로 받은 함수의 반환값의 타입 파라메터인 `b`를 가진다.

### 예제
```js
let safeInc = R.unless(R.isNil, R.inc);
safeInc(null); //=> null
safeInc(1); //=> 2
```
- `R.unless` 함수는 첫 번째 인자로 술어함수 `R.isNil`을 받고, 두 번째 인자로 인자로 받은 값에 1을 더한 결과를 반환하는 `R.inc` 함수를 받는다.
- `safeInc`는 `R.unless`가 세 번째 인자를 받을 수 있도록 하는 함수가 되며, `safeInc(null)`는 세 번째 인자를 받아서 술어함수 `R.isNil`를 참으로 만족하므로 그대로의 값 `null`을 반환하고, `safeInc(1)`는 술어함수 `R.isNil`를 만족하지 못하므로 두 번째로 받은 인자 `R.inc`에 값을 전달한 값을 최종적으로 얻는다. 따라서 1이 전달 되었으므로 2를 반환한다.

## References
- https://ramdajs.com/docs/#unless
