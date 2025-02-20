## complement

> Takes a function f and returns a function g such that if called with the same arguments when f returns a "truthy" value, g returns false and when f returns a "falsy" value g returns true.
- 함수 f를 받아 함수 g를 반환한다. 만약 동일한 인자로 호출된다면 f가 "참(truthy)" 값을 반환할 때 g는 `false`를 반환하고, f가 "거짓(falsy)" 값을 반환할 때 g는 `true`을 반환한다.
> R.complement may be applied to any functor
- R.complement는 어떠한 펑터에도 적용될 수 있다.
> See also [not](./not.md).

## 설명

- 임의의 동일한 인자에 대해 주어진 함수의 참 거짓의 결과를 반대로 내는 새로운 함수를 만든다.
- `complement`란 말은 집합이론에서 여집합을 의미한다.
- A, B는 불리언 타입이다. 정의역 x에 대해 함수 f를 적용한 결과가 A일 때, 정의역 x에 대해 complement(f)를 적용한 결과가 B일 때, 동일한 정의역의 원소 a에 대해 f와 complement(f)는 서로 다른 불리언 값을 갖는다. A가 true이면 B는 false이고 A가 false이면 B는 true가 된다.

## 문법

```
R.complement(f): function
```
> f
- f : 임의의 함수를 받는다.
> Returns function
- 함수를 반환한다. f에 전달한 결과 값과 동일한 인자를 전달 받았을 때 f가 반환하는 값이 아닌 불리언 값을 반환한다.

## 표현

```
(*… → *) → (*… → Boolean)
```
- `(*… → *) →`: `*…` 임의의 갯수와 타입의 인자를 받아 `*` 임의의 종류의 단일한 결과값을 내는 함수를 하나 받는다.
- `→ (*… → Boolean)`: 반환된 함수는 `*…` 마찬가지로 첫 번재 받은 함수가 받을 수 있는 인자와 동일한 인자를 받아 첫 번째 인자로 받은 함수의 결과값과 반대로 참 거짓을 반환한다.

## 예제

```js
const isNotNil = R.complement(R.isNil);
R.isNil(null); //=> true
isNotNil(null); //=> false
R.isNil(7); //=> false
isNotNil(7); //=> true
```
- `isNotNil`은 `R.isNil` 함수가 받는 값을 받을 때 결과 값이 반대가 된다. 어떤 인자에 대해 `R.isNil`이 true를 반환하면 `isNotNil`는 false를 반환하며, `R.isNil`이 false 반환하면 `isNotNil`는 true를 반환한다.
- `R.isNil`은 `null` 또는 `undefined`를 확인하는 함수이다.
- `R.isNil`이 참을 반환할 때 `isNotNil`는 false를 반환하고 `R.isNil`이 거짓을 반환할 때 `isNotNil`는 true를 반환한다.
- `R.isNil(null)`은 true을 반환하므로 `isNotNil(null)`은 false을 반환한다.
- `R.isNil(7)`은 false을 반환하므로 `isNotNil(7)`는 true를 반환한다.

## References
- https://ramdajs.com/docs/#complement
- https://stackoverflow.com/questions/51662504/why-was-complement-used-as-a-name-for-the-function-in-ramda-js
- https://en.m.wikipedia.org/wiki/Complement_(set_theory)
