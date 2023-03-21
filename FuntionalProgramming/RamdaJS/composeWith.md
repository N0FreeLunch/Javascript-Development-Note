## composeWith
> Performs right-to-left function composition using transforming function. The last function may have any arity; the remaining functions must be unary.
- 변환 함수를 사용하여 오른쪽에서 왼쪽으로 함수 합성한다. 마지막 인자로 받는 함수는 다양한 갯수의 인자를 받을 수 있으며, 마지막 인자로 받는 함수가 아닌 나머지 위치에서 인자로 받는 함수들은 인자를 하나만 갖는 함수이어야 한다.
> Note: The result of composeWith is not automatically curried. Transforming function is not used on the last argument.
- 참고: `composeWith`의 결과는 자동으로 커링되지 않는다. 또한 변환함수는 마지막 인자로 받는 함수에는 사용되지 않는다.
> See also compose, pipeWith.

## 설명
- `composeWith` 함수는 `compose` 함수와 달리 차례로 함성할 함수와 이전 함수의 결과값을 파라메터로 받아 정의된 로직을 실행한 결과를 다음 합성에 사용한다.
- 첫 번째 인자로는 함수를 받는다. 이 함수는 오른쪽에서 왼쪽으로 함수를 합성할 때 오른쪽의 함수를 첫 번째 파라메터로 받고 왼쪽에서 넘어온 합성된 결과 값를 두 번째 파라메터로 받는 함수이다.

## 표현
```
((* → *), [(y → z), (x → y), …, (o → p), ((a, b, …, n) → o)]) → ((a, b, …, n) → z)
```
- `((* → *), [(y → z), (x → y), …, (o → p), ((a, b, …, n) → o)]) →`
- `→ ((a, b, …, n) → z)`

## 예제
```
const composeWhileNotNil = R.composeWith((f, res) => R.isNil(res) ? res : f(res));

composeWhileNotNil([R.inc, R.prop('age')])({age: 1}) //=> 2
composeWhileNotNil([R.inc, R.prop('age')])({}) //=> undefined
```
- `composeWhileNotNil([R.inc, R.prop('age')])({})` 부분의 로직을 보면 `R.prop('age')({})`한 결과는 `undefined`가 된다. 그런데 이 결과에 `R.inc`라는 함수를 적용해 버리면 에러가 발생한다. 이런 에러를 방지하기 위해서는 하나의 함수를 합성하는 절차에서 전달된 결과가 다음 함수와 합성될 수 있는지 확인해 주는 중간 과정이 필요하다. 이를 위한 중간의 함수를 받는데 `R.composeWith`의 첫 번째 인자로 받는 함수가 이런 역할을 한다.

## Reference
- https://ramdajs.com/docs/#composeWith
