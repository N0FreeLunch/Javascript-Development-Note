## pipeWith
> Performs left-to-right function composition using transforming function. The first function may have any arity; the remaining functions must be unary.
- 왼쪽에서 오른쪽으로 변환 함수를 사용하여 함수를 나열한 순대로 합성한다. 첫 번째 함수는 임의의 수의 인자의 갯수를 가질 수 있지만, 나머지 함수는 반드시 인자를 하나 갖는 함수여야 한다.

> Note: The result of pipeWith is not automatically curried. Transforming function is not used on the first argument.
- 노트 : pipeWith의 결과는 자동적으로 커링되어 있지 않다. 변환 함수는 첫 번째 인자에 할당할 수 없다.

> See also composeWith, pipe.

### 설명

### 표현
```
((* → *), [((a, b, …, n) → o), (o → p), …, (x → y), (y → z)]) → ((a, b, …, n) → z)
```

### 예제
```js
const pipeWhileNotNil = R.pipeWith((f, res) => R.isNil(res) ? res : f(res));
const f = pipeWhileNotNil([Math.pow, R.negate, R.inc])

f(3, 4); // -(3^4) + 1
```
- `pipeWhileNotNil`라는 이름은 함수를 합성할 때 전달 받은 결과가 null이 아닌 경우에만 합성을 하도록 한다는 의미를 가지고 있다.
- `(f, res) => R.isNil(res) ? res : f(res)`는 변환 함수에 해당하며, 함수를 합성할 때 이전 함수의 결과 값이 `res`에 해당하며, 합성할 대상 합수를 f로 한다. 변환 함수를 t라고 해 보자.
- `Math.pow(3, 4)`이므로 `3^4`가 되고, 함성을 수행할 때 변환 함수를 통해서 합성을 수행하므로 `t(R.negate, 3^4)`의 코드가 실행된다. `3^4`가 null이 아니므로 `f(res)`를 실행하므로 `R.negate(3^4)`이다.

## Reference
- https://ramdajs.com/docs/#pipeWith
