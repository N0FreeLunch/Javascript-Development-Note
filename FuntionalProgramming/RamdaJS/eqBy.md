## eqBy
> Takes a function and two values in its domain and returns true if the values map to the same value in the codomain; false otherwise.

## 표현
```
(a → b) → a → a → Boolean
```
- `(a → b) →` 첫 번째 인자로 함수를 할당한다.
- `→ a → a →` 두 번째 인자와 세 번째 인자로 첫 번째 함수의 인자와 동일한 타입의 값을 할당한다.
- `→ Boolean` 결과 값으로 참 거짓을 반환한다.

## 설명
- 첫 번째 인자로 인자를 하나 받는 함수를 넣는다.
- 두 번째 인자와 세 번째 인자로 첫 번째 인자에 할당한 함수의 인자로 할당할 수 있는 값을 할당한다.
- 주어진 함수에 두 번째 인자와 세 번째 인자를 할당해 평가한 결과 값이 같은지 확인한다.

## 예제
```
R.eqBy(Math.abs, 5, -5); //=> true
```
- `R.eqBy(Math.abs, 5, -5)`의 의미는 `Math.abs(5) == Math.abs(-5)`와 동일한 의미를 같는다. 따라서 참을 반환한다.

## Reference
- https://ramdajs.com/docs/#eqBy
