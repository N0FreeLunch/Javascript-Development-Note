## composeWith

> Performs right-to-left function composition using transforming function. The last function may have any arity; the remaining functions must be unary.
- 변환 함수를 사용하여 오른쪽에서 왼쪽으로 함수 합성한다. 마지막 인자로 받는 함수는 다양한 갯수의 인자를 받을 수 있으며, 마지막 인자로 받는 함수가 아닌 나머지 위치에서 인자로 받는 함수들은 인자를 하나만 갖는 함수이어야 한다.
> Note: The result of composeWith is not automatically curried. Transforming function is not used on the last argument.
- 참고: `composeWith`의 결과는 자동으로 커링되지 않는다. 또한 변환 함수(Transforming function)는 마지막 인자로 받는 함수에는 사용되지 않는다.
> See also [compose](./compose.md), [pipeWith](./pipeWith.md).

### 설명

- `composeWith` 함수는 `compose` 함수와 달리 차례로 함성할 함수와 이전 함수의 결과값을 파라메터로 받아 정의된 로직을 실행한 결과를 다음 합성에 사용한다.
- 첫 번째 인자로는 함수를 받는다. 이 함수는 오른쪽에서 왼쪽으로 함수를 합성할 때 오른쪽의 함수인 합성할 함수를 첫 번째 파라메터로 받고 왼쪽에서 넘어온 합성되면서 연산되어 전달된 결과 값를 두 번째 파라메터로 받는 함수이다.
- 함수를 합성하기 위해서는 다음 함수로 전달되는 값이 다음 함수의 인자로 사용될 수 있는 것이어야 한다. 만약 사용될 수 없는 값이라면 함성을 하지 않고 다른 처리를 해야 할 수 있다. `composeWith` 함수는 함수를 합성하기 전에 미리 적용될 수 있는 값인지 아닌지 검사를 하고 이에 따른 처리를 달리 하게 할 수 있다는 장점이있다. 또한 함수를 합성하다가 어떤 예외적인 값에 대해서는 보정을 해서 전달할 필요가 있을 수 있는데 이런 경우에도 사용하기 좋다.
- `compose`함수는 여러 함수를 순차적으로 합성 시킨다. `composeWith`는 이전 합성 결과에 다음 합성 함수를 적용시킬 때의 로직을 정한다. 다양한 함수에 적용하는 만큼 이전 결과에 다음 함수를 합성할 때 미리 적용해야 하는 로직은 다양할 수 있다. 하지만 `composeWith`는 하나의 함수만을 설정하기 때문에 각 함수가 합성이 될 때 합성 각각에 적용이 되는 로직 보다는 여러 함수의 합성 과정에서 공통으로 처리하고 싶은 로직이 있을 때 사용하는 것이 좋다.

### 문법

```
R.composeWith(transformer, functions): function
```
> `transformer`: The transforming function
- `transformer`: 변환 함수
> `functions`: The functions to compose
- `functions`: 합성할 함수들
> Returns function
- 함수를 반환한다.

### 표현
```
((* → *), [(y → z), (x → y), …, (o → p), ((a, b, …, n) → o)]) → ((a, b, …, n) → z)
```
- `((* → *), [(y → z), (x → y), …, (o → p), ((a, b, …, n) → o)])`: 먼저 변형 함수와 합성할 함수 리스트를 받는다. 첫 번째 인자인 `(* → *)` 부분은 변형 함수에 해당하는데 `(* → *)`으로 인자를 하나 받아서 하나의 인자를 반환하는 함수로 구성되어 있다. 두 번째 인자인 `[(y → z), (x → y), …, (o → p), ((a, b, …, n) → o)] →` 부분을 보면 `compose` 함수와 비슷하게 함성할 함수를 받는다. `compose`는 인자로 합성할 함수 리스트를 받는 반면, `composeWith`는 합성할 함수를 배열의 원소로 나열해 받는다. 오른쪽에서 왼쪽으로 함수를 차례로 합성하는데 맨 오른쪽 마지막 함수는 임의의 인자의 갯수를 받는 함수이지만, 나머지 함수들은 인자를 하나만 받아서 평가되는 함수로 구성된다. 또한 리스트의 인자의 구성을 보면 오른쪽에서 반환된 타입이 바로 왼쪽 함수의 파라메터 타입이 된다는 것을 알 수 있다. `((* → *), [(y → z), (x → y), …, (o → p), ((a, b, …, n) → o)])` 변형 함수와, 함수 리스트 두 개의 인자 세트를 받으면 `((a, b, …, n) → z)`라는 하나의 함수가 평가되어 나온다.
- `→ ((a, b, …, n) → z)`: 이 함수는 모든 함수의 합성된 결과물이기 때문에 함수를 합성할 때의 첫 번째 함수가 받는 인자와 동일한 인자 구성을 받는다. 두 번째 인자로 받은 리스트의 마지막 함수인 `(a, b, …, n) → o)`와 동일한 인자를 받고 리스트의 첫 번째 함수가 반환하는 `→ z`라는 타입을 최종 결과 타입으로 가진다는 것을 알 수 있다.

### 예제
```js
const composeWhileNotNil = R.composeWith((f, res) => R.isNil(res) ? res : f(res));

composeWhileNotNil([R.inc, R.prop('age')])({age: 1}) //=> 2
composeWhileNotNil([R.inc, R.prop('age')])({}) //=> undefined
```
- `composeWhileNotNil([R.inc, R.prop('age')])({})` 부분의 로직을 보면 `R.prop('age')({})`한 결과는 `undefined`가 된다. 그런데 이 결과에 `R.inc`라는 함수를 적용해 버리면 에러가 발생할 수 있다. 물론 `R.inc`란 함수는 수가 아닌 대상이 오면 `NaN`으로 변환한다. 하지만 도중에 잘못된 값이 전달되어 연산이 실패하는 `NaN`보다는 값 자체가 없다는 것을 확실하게 알 수 있게 하는 것이 좋으므로 `null`, `undefined`의 경우에는 그대로 표현하는 것이 좋을 수 있다.
- 이를 위해서는 하나의 함수를 합성하는 절차에서 전달된 결과가 다음 함수와 합성될 수 있는지 확인해 주는 중간 과정이 필요하다. 이를 위해서 중간의 함수를 받는데 `R.composeWith`의 첫 번째 인자로 받는 함수가 이런 역할을 한다.
- `R.composeWith((f, res) => R.isNil(res) ? res : f(res))` 부분을 보면 `(f, res) => R.isNil(res) ? res : f(res)`라는 함수를받는다. 이 함수는 전달된 값이 `null`또는 `undefined`이면 다음으로 합성할 함수 `f`를 합성하지 않고 값이 세팅되어 있으면 함수 `f`를 합성하는 로직을 가지고 있다. `R.inc`는 수를 받아서 그 값을 1 증가시키는 함수이다.
- `NaN`이 아니라 `undefined`가 결과로 나왔으므로 연산의 에러 부분이 아닌, 전달된 값이 `undefined`인지 확인을 하게 된다. 또한 함수의 합성에는 이전에 합성된 결과에 다음 함수를 적용시킬 수 있는 값이 와야 하는 것을 보증할 수 있어야 한다. 이런 보증을 위해서 사용하는 함수로 볼 수 있다.
- `composeWhileNotNil([R.inc, R.prop('age')])({age: 1})` 부분을 보면 수가 `R.inc` 함수에 전달되었으므로 받은 수 1이 2가 된 결과를 반환한다.

## References
- https://ramdajs.com/docs/#composeWith
- https://github.com/ramda/ramda/blob/master/test/composeWith.js
- https://github.com/ramda/types/blob/develop/types/composeWith.d.ts
