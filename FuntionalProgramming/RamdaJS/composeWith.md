## composeWith
> Performs right-to-left function composition using transforming function. The last function may have any arity; the remaining functions must be unary.
- 변환 함수를 사용하여 오른쪽에서 왼쪽으로 함수 합성한다. 마지막 인자로 받는 함수는 다양한 갯수의 인자를 받을 수 있으며, 마지막 인자로 받는 함수가 아닌 나머지 위치에서 인자로 받는 함수들은 인자를 하나만 갖는 함수이어야 한다.
> Note: The result of composeWith is not automatically curried. Transforming function is not used on the last argument.
- 참고: `composeWith`의 결과는 자동으로 커링되지 않는다. 또한 변환함수는 마지막 인자로 받는 함수에는 사용되지 않는다.
> See also compose, pipeWith.

## 설명

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

## Reference
- https://ramdajs.com/docs/#composeWith
