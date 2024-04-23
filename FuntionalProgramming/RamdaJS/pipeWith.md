## pipeWith
> Performs left-to-right function composition using transforming function. The first function may have any arity; the remaining functions must be unary.
- 변환 함수를 사용하여 왼쪽에서 오른쪽으로 함수를 나열한 순대로 합성한다. 첫 번째 함수는 임의의 수의 인자의 갯수를 가질 수 있지만, 나머지 함수는 반드시 인자를 하나 갖는 함수여야 한다.

> Note: The result of pipeWith is not automatically curried. Transforming function is not used on the first argument.
- 노트 : pipeWith의 결과는 자동적으로 커링되어 있지 않다. 변환 함수는 첫 번째 인자에 할당할 수 없다.

> See also composeWith, pipe.

### 설명
- pipe으로 함수를 합성할 때 변환함수라는 것을 함수의 합성 방식을 정할 수 있는 기능이다.
- 첫 번째 인자로는 변환 함수를 정의한다. 변환 함수의 첫 번째 인자는 다음으로 합성할 함수를 받고, 두 번째 인자로는 해당 지점의 함수에 값이 전달되어 평가된 결과값이 주어진다. 변환 함수를 t라고 하면 t를 다음과 같이 정의할 수 있다. t(다음으로 합성할 함수, 이전까지 함수들이 파이프를 통해서 생성한 결과 값)
- 두 번째 인자로는 합성할 함수를 차례로 나열한다. 나열된 순으로 왼쪽에서 오른쪽으로 합성한다.
- 반환된 결과값은 함성된 함수이며 값을 받아 평가될 수 있다.

### 표현
```
((* → *), [((a, b, …, n) → o), (o → p), …, (x → y), (y → z)]) → ((a, b, …, n) → z)
```
- `((* → *), [((a, b, …, n) → o), (o → p), …, (x → y), (y → z)]) →`: 첫 번재 인자(`(* → *)`)와 두 번째 인자(`[((a, b, …, n) → o), (o → p), …, (x → y), (y → z)]`)를 받아서 평가된다는 의미로 (첫 번째 인자, 두 번째 인자) 꼴으로 괄호로 묶였다.
- `(* → *)`: 변환 함수에 해당한다. (변환 함수의 첫 번째 인자는 합성할 함수를 두 번째 인자로는 이전 함수에서 전달된 값을 받는 의미하는데 이에 대한 구분감 없이 `* → *`으로 표기한 것은 이상함, 아마도 `→ o`, `→ p` 등의 결과를 받을 수 있고, 함수 `(o → p)`, `(y → z` 등을 받을 수 있기 때문에 특정한 종류로 표현하기 모호한 면이 있어 *를 사용한 표기를 한 것으로 보임)
- `[((a, b, …, n) → o), (o → p), …, (x → y), (y → z)]`: 합성할 함수를 나열한다. 첫 번째 함수는 여러개의 인자를 받을 수 있지만, 그 다음 함수는 이전 함수의 결과 값을 받아 평가 되어야 하므로 하나의 인자만을 받도록 되어 있다.
- `→ ((a, b, …, n) → z)`: 합성된 함수를 반환한다. 합성된 함수는 합성할 함수 리스트의 첫 번째 함수가 받는 인자를 받아 평가되어 그 결과를 다음 함수에 전달하는 방식으로 이뤄지므로 합성할 함수 리스트의 첫 번재 함수가 받는 인자와 동일한 인자를 받는다.

### 예제
```js
const pipeWhileNotNil = R.pipeWith((f, res) => R.isNil(res) ? res : f(res));
const f = pipeWhileNotNil([Math.pow, R.negate, R.inc])

f(3, 4); // -(3^4) + 1
```
- `pipeWhileNotNil`라는 이름은 함수를 합성할 때 전달 받은 결과가 null이 아닌 경우에만 합성을 하도록 한다는 의미를 가지고 있다.
- `(f, res) => R.isNil(res) ? res : f(res)`는 변환 함수에 해당하며, 함수를 합성할 때 이전 함수의 결과 값이 `res`에 해당하며, 합성할 대상 합수를 f로 한다. 변환 함수를 t라고 해 보자.
- `Math.pow(3, 4)`이므로 `3^4`가 되고, 함성을 수행할 때 변환 함수를 통해서 합성을 수행하므로 `t(R.negate, 3^4)`의 코드가 실행된다. `3^4`가 null이 아니므로 `f(res)`를 실행하므로 `R.negate(3^4)`이다. 결과값인 `-3^4`와 함수 `R.inc`를 합성을 할 때 변환 함수에 의해 `t(R.inc, -3^4)`의 코드가 실행된다. `-3^4`은 null이 아니므로 `f(res)` 부분의 코드가 실행되므로 `R.inc(-3^4)`이다. 최종 결과 값은 `-(3^4) + 1`가 된다.
- 만약 `const g = pipeWhileNotNil([Math.pow, (v) => null, R.negate, R.inc])`으로 중간에 `(v) => null`을 넣으면 `g(3, 4)`의 결과는 `(v) => null`에 의해 결과값이 null이 되기 때문에 변환 함수 t에 의해서 `R.isNil(res) ? res : f(res))`의 `res` 부분이 반환된다. 변환 함수에 의해 `t(R.negate, null)`의 결과는 null이 되고, 이 null을 전달 받아 `t(R.inc, null)`이 되어 null이 반환되어 최종 값은 null이 된다.

## Reference
- https://ramdajs.com/docs/#pipeWith
