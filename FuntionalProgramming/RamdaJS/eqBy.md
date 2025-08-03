## eqBy
> Takes a function and two values in its domain and returns true if the values map to the same value in the codomain; false otherwise.
- 하나의 함수를 받아, 그 함수의 정의역(domain)에 속하는 두 값을 인자로 취해, 그 값들을 공역(codomain)의 같은 값으로 매핑할 경우 true를 반환하고, 그렇지 않으면 false를 반환한다.

## 설명

- 첫 번째 인자로 인자를 하나 받는 함수를 넣는다.
- 두 번째 인자와 세 번째 인자로 첫 번째 인자에 할당한 함수의 인자로 할당할 수 있는 값을 받는다.
- 주어진 함수를 f, 두 번째 인자를 x, 세 번째 인자를 y라고 할 때, f(x), f(y) 두 결과를 비교하여 그 값이 같은지를 확인한다.

## 문법

```
R.eqBy(f, x, y): Boolean
```
> f
- f: 정의역과 공역이 정해져 있으며, 공역의 값을
> x
- x: 정의역의 어떤 값 x
> y
- y: 정의역의 어떤 값 y
> Returns Boolean
> 불리언 타입의 값을 반환한다.

## 표현

```
(a → b) → a → a → Boolean
```

- `(a → b) →` 첫 번째 인자로 함수를 할당한다.
- `→ a → a →` 두 번째 인자와 세 번째 인자로 첫 번째 함수의 인자와 동일한 타입의 값을 할당한다.
- `→ Boolean` 결과 값으로 참 거짓을 반환한다.

## 예제

```js
R.eqBy(Math.abs, 5, -5); //=> true
```
- `R.eqBy(Math.abs, 5, -5)`의 의미는 `Math.abs(5) == Math.abs(-5)`와 동일한 의미를 같는다. 따라서 참을 반환한다.

## References
- https://ramdajs.com/docs/#eqBy
- https://github.com/ramda/ramda/blob/master/test/eqBy.js
- https://github.com/ramda/types/blob/develop/types/eqBy.d.ts
