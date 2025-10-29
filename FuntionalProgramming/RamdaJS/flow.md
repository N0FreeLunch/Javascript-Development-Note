# flow

> Takes the value of an expression and applies it to a function which is the left-to-right serial composition of the functions given in the second argument.

> The functions in the pipeline should be unary functions.

> flow is helps to avoid introducing an extra function with named arguments for computing the result of a function pipeline which depends on given initial values. Rather than defining a referential transparent function f = (_x, _y) => R.pipe(g(_x), h(_y), …) which is only later needed once z = f(x, y), the introduction of f, _x and _y can be avoided: z = flow(x, [g, h(y),…]

> In some libraries this function is named pipe.

> See also [pipe](./pipe.md).

## 설명

- `pipe` 함수가 함수의 합성만을 하는 것이라면, `flow`는 함수의 합성과 시드값을 함께 나열하여 보여주기 위한 문법을 가지고 있다.

## 문법

```
R.flow(a, pipeline): *
```

> `a`: The seed value
- `a`: 시드 값

> `pipeline`: functions composing the pipeline
-`pipeline`: 합성할 파이프 라인 functions (타입이 `function[]`으로 원소를 함수로 하는 배열)

> Returns * z The result of applying the seed value to the function pipeline
- 시드 값이 적용된 함수 파이프라인의 결과

## 표현

```
a → [(a → b), …, (y → z)] → z
```
- `a →`: 함성된 파이프라인에 전달할 값으로 시드값으로 부른다.
- `[(a → b), …, (y → z)]`: 함수의 파이프라인을 나열한 배열로, 첫 번째 함수는 시드 값을 받을 수 있도록 a 종류의 값을 받을 수 있는 `(a → b)` 함수가 위치한다.
- `→ z`: 파이프라인의 최종 연산 결과 값이 반환되는 것으로 파이프 라인에 나열된 마지막 함수의 최종 반환값 종류와 같은 종류의 값이 반환된다.

## 예시

```js
R.flow(9, [Math.sqrt, R.negate, R.inc]); //=> -2

const personObj = { first: 'Jane', last: 'Doe' };
const fullName = R.flow(personObj, [R.values, R.join(' ')]); //=> "Jane Doe"
const givenName = R.flow('    ', [R.trim, R.when(R.isEmpty, R.always(fullName))]); //=> "Jane Doe"
```

- `R.flow(9, [Math.sqrt, R.negate, R.inc])`: 전달된 값의 제곱근을 구하고 (`Math.sqrt`), 반대 부호를 붙여주고(`R.negate`), 값을 1 증가(`R.inc`)시킨다. 시드 값이 9가 전달되었으므로 제곱근은 3, 반대 부호는 -3. 값을 1 증가시키면 -2가 된다.

## References

- https://ramdajs.com/docs/#flow
- https://github.com/ramda/ramda/blob/master/test/flow.js
- https://github.com/ramda/types/blob/develop/types/flow.d.ts
