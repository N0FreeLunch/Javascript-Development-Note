# flow

> Takes the value of an expression and applies it to a function which is the left-to-right serial composition of the functions given in the second argument.
- 나타내려는 값을 받고, 두번째 인자에 (함수가 나열된 배열로) 주어진 함수들을 왼쪽에서 오른쪽으로 연속하여 합성된 함수에 (해당 값을) 적용한다.

> The functions in the pipeline should be unary functions.
- (나열되는 파이프라인의) 함수들은 단항 함수여야 한다.

> flow is helps to avoid introducing an extra function with named arguments for computing the result of a function pipeline which depends on given initial values.
- flow (함수)는 (파이프라인에 전달하기 위해 별도의 함수를 정의하여 해당 함수의 이름을 전달하는 등의 중간 함수를 정의하는 것과 같은) 여분의 함수를 도입하는 것을 피하는 것에 도움을 줄 수 있다. 이 여분의 함수는 주어진 초기 값들에 의존하는 (특정 맥락 또는 한 번만 사용하기 위한 값을 변환하기 위해서 사용되는) 파이프라인 함수의 결과를 계산하기 위해 (외부에서 정의한 함수를 파이프라인의 인자로 전달하기 위해 함수명을 사용하는 것으로) 이름 붙여진 인자를 정의하는 것과 같은 것이다.

> Rather than defining a referential transparent function f = (_x, _y) => R.pipe(g(_x), h(_y), …) which is only later needed once z = f(x, y), the introduction of f, _x and _y can be avoided: z = flow(x, [g, h(y),…]
- 참조 투명한 함수 `f = (_x, _y) => R.pipe(g(_x), h(_y), …)`와 같은 것을 정의하는 것 보다, `z = flow(x, [g, h(y),…]`으로 (이와 같은 방식으로 사용하여), 그저 나중에 한 번의 필요한 (정의하는) `z = f(x, y)`(와 같은 함수를 만들어), f (함수명), _x, _y(해당 함수의 파라메터)의 (보일러플레이트) 도입을 피할 수 있다.

> In some libraries this function is named pipe.
- 몇몇 라이브러리에서 이 함수는 pipe라고 부른다.

> See also [pipe](./pipe.md).

## 설명

- `pipe` 함수가 함수의 합성만을 하는 것이라면, `flow`는 함수의 합성과 합성한 함수에 적용할 시드값을 함께 나열하여 보여주기 위한 문법을 가지고 있다. 재사용할 필요가 없는 특정 맥락에서 한 번만 사용하기 위한 함수를 `pipe`와 같은 함수로 별도의 합성 함수를 정의할 필요없이, 람다식으로 간략히 사용할 수 있게 하기 위한 용도로 사용된다.
- 첫 번째 인자로는 변환할 초기값을 받는다.
- 두 번째 인자로는 초기값을 적용할 순서대로 나열된 함수 리스트를 받는다.
- 먼저 나열된 함수를 먼저 초기값에 적용하고, 적용된 결과를 다음 함수의 인자로 전달하는 파이프라인의 흐름이지만, 초기값을 적용하기 전에 먼저 함수를 합성하고, 합성된 함수의 결과에 초기값을 적용하는 방식으로 구성된다.

## 문법

```
R.flow(a, pipeline): *
```

> `a`: The seed value
- `a`: 시드 값

> `pipeline`: functions composing the pipeline
- `pipeline`: 합성할 파이프 라인 functions (타입이 `function[]`으로 원소를 함수로 하는 배열)

> Returns * z The result of applying the seed value to the function pipeline
- 어떠한 종류의 값이든 반환될 수 있다. 이 반환값은 (마지막 함수의 반환 종류인) z이다. 시드 값이 적용된 함수 파이프라인의 결과

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

- `const fullName = R.flow(personObj, [R.values, R.join(' ')])`: 오브젝트 프로퍼티의 값을 나열한 배열을 반환하고(`R.values`), 배열의 값을 공백으로 연결한 문자열을 만드는(`R.join(' ')`) 파이프라인에 `personObj` = ` { first: 'Jane', last: 'Doe' }`를 전달한다. 그래서 프로퍼티 값만 뽑아 연결하면 ` "Jane Doe"`가 되는 것

- `R.flow('    ', [R.trim, R.when(R.isEmpty, R.always(fullName))])`: 값의 좌우의 공백을 제거(`R.trim`)하고, 전달된 값이 빈 값일 때 (`R.isEmpty`), 디폴트 값으로 `fullName` 변수의 값을 다음을 전달(`R.always(fullName)`)한다. 시드 값으로 `'    '`이 전달되어, 공백이 제거되고, 공백이 제거되면 빈 문자열이 되고, 빈 값인 경우, `fullName` 값을 반환하게 되므로 `"Jane Doe"`가 반환된다.

## References

- https://ramdajs.com/docs/#flow
- https://github.com/ramda/ramda/blob/master/test/flow.js
- https://github.com/ramda/types/blob/develop/types/flow.d.ts
