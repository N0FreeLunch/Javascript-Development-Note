## complement
> Takes a function f and returns a function g such that if called with the same arguments when f returns a "truthy" value, g returns false and when f returns a "falsy" value g returns true.
- 함수 f를 받아 함수 g를 반환합니다. 만약 동일한 인자로 호출된다면 f가 "참(truthy)" 값을 반환할 때 g는 `false`를 반환하고, f가 "거짓(falsy)" 값을 반환할 때 g는 `true`을 반환합니다.
- "truthy"는 자동 형변환으로 true로 판별될 수 있는 값을 의미하며 "falsy"는 자동 형변환으로 false를 판별할 수 있는 값을 의미한다.
> R.complement may be applied to any functor
- R.complement는 어떠한 펑터에도 적용될 수 있다.
> See also not.

## 설명
- 임의의 동일한 인자에 대해 주어진 함수의 참 거짓의 결과를 반대로 내는 새로운 함수를 만든다.
- `complement`란 말은 집합이론에서 여집합을 의미한다. `complement`에 디스패치 되기 전의 함수가 임의의 인자 x에 대해 참을 반환했다면 `complement`에 디스패치 되고 난 후의 함수는 x가 아닌 값에 대한 참을 반환하는 함수로 바뀐다. 곧 값 x와 x가 아닌 값으로 나뉘므로 둘의 관계는 여집합의 관계가 된다.

## 표현
```
(*… → *) → (*… → Boolean)
```
- `(*… → *) →`는 `*…` 하나 또는 여러개의 인자를 받아 `*` 어떤 단일한 결과값을 내는 함수를 하나 받는다.
- `→ (*… → Boolean)` 반환된 함수는 `*…` 마찬가지로 첫 번재 받은 함수가 받을 수 있는 인자와 동일한 인자를 받아 참 거짓을 반환한다.

## 예제
```
const isNotNil = R.complement(R.isNil);
R.isNil(null); //=> true
isNotNil(null); //=> false
R.isNil(7); //=> false
isNotNil(7); //=> true
```
- `R.isNil`은 `null` 또는 `undefined`를 확인하는 함수이다.
- `R.isNil`이 참을 반환할 때 `isNotNil`는 false를 반환하고 `R.isNil`이 거짓을 반환할 때 `isNotNil`는 true를 반환합니다.
- `R.isNil(null)`은 참을 반환하므로 `isNotNil(null)`은 거짓을 반환한다.
- `R.isNil(7)`은 거짓을 반환하므로 `isNotNil(7)`는 참을 반환한다.

## Reference
- https://ramdajs.com/docs/#complement
- https://stackoverflow.com/questions/51662504/why-was-complement-used-as-a-name-for-the-function-in-ramda-js
- https://en.m.wikipedia.org/wiki/Complement_(set_theory)
