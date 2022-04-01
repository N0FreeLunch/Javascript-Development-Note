## ap
- `R.ap()`
- applies 라는 뜻을 가진 함수

## 설명
- '가장 마지막 인자'를 그 '바로 이전 인자의 함수'의 인자로 넣으며 이 '인자를 넣은 함수'를 '그 이전 인자인 함수'에 넣는 방식으로 되어 있다.

## 표현
### 배열을 인자로 사용할 때
```
`[a → b] → [a] → [b]`
```
- `a → b` 하나의 인자를 넣으면 평가하여 결과 값을 만들어내는 함수를
- `[a → b]` 배열에 넣는다.
- `[a → b] → [a]` 다음 인자로 `[a]`를 받으며
- `→ [b]` 결과값을 배열 형태로 받는다.

### 함수를 인자로 사용할 때
```
Apply f => f (a → b) → f a → f b
```
- `f`는 커링된 함수를 의미한다. 인자를 하나 받으면 평가될 수 있는 함수를 의미한다. 
- `Apply f`는 `R.ap()` 함수의 첫번째 인자로 커링된 함수를 받는다는 의미이다.
- `=> f (a → b)`는 `R.ap()`의 첫 번째로 받은 함수 f에 두 번째로 받은 인자인 `a → b` 함수를 인자로 집어 넣는다. 그러면 `f a`란 커링된 함수를 반환한다.
- `→ f a` 인자로 a 값을 받았을 때
- `→ f b` 인자로 b 값을 받는 함수를 반환한다.

### 
```
(r → a → b) → (r → a) → (r → b)
```

## 예제
```
R.ap([R.multiply(2), R.add(3)], [1,2,3]); //=> [2, 4, 6, 4, 5, 6]
```
- 배열을 첫번째 인자로 받기 때문에 두 번째 인자도 배열로 받는다.
- `R.multiply(2)`는 수 하나를 원소로 받아 2를 곱하는 함수이다. `R.add(3)`은 수 하나를 원소를 받아 3을 더하는 함수이다.
- `R.ap([R.multiply(2), R.add(3)]);`에서 `R.ap()` 함수는 인자로 받는 `[R.multiply(2), R.add(3)]` 리스트 안의 함수를 `R.ap` 함수의 다음 인자로 받는 대상을 적용한 결과 값으로 대체한다.
- `R.ap([R.multiply(2), R.add(3)], [1,2,3]);`에서 `[1,2,3]`의 각 원소에 `R.multiply(2)`을 적용하여 나온 결과값 `2`, `4`, `6`을 `[R.multiply(2), R.add(3)]`의 `R.multiply(2)` 대신 `R.add(3)`를 거용하여 나온 결과값 `4`, `5`, `6`으로 대체한다.
- 따라서 `[R.multiply(2), R.add(3)]`이 `[2, 4, 6, 4, 5, 6]`이란 결과가 나온다.

```
R.ap([R.concat('tasty '), R.toUpper], ['pizza', 'salad']); //=> ["tasty pizza", "tasty salad", "PIZZA", "SALAD"]
```
- 배열을 첫번째 인자로 받기 때문에 두 번째 인자도 배열로 받는다.
- `R.concat('tasty ')`는 문자열 하나를 받아서 `tasty ` 문자열 뒤에 주어진 문자 원소를 받아서 반환하는 함수이다.
- `R.toUpper`는 주어진 문자열 하나를 받아서 소문자를 대문자로 바꾼다.
- `R.ap([R.concat('tasty '), R.toUpper], ['pizza', 'salad']);`에서 `R.concat('tasty ')`를 `['pizza', 'salad']`을 인자로 받아 `'tasty pizza'`, `'tasty salad'`를 만들어내고 `R.toUpper`를 `['pizza', 'salad']`에 적용하여 `"PIZZA"`, `"SALAD"`를 만들어 낸다.
- 이를 리스트의 위치에 대체하여 `["tasty pizza", "tasty salad", "PIZZA", "SALAD"]`이란 결과를 만들어 낸다.

```
// R.ap can also be used as S combinator
// when only two functions are passed
R.ap(R.concat, R.toUpper)('Ramda') //=> 'RamdaRAMDA'
```
- 함수를 첫번째 인자로 받기 때문에 두 번째 인자도 함수로 받는다.
- `R.ap(R.concat, R.toUpper)`의 함수를 넣게 되면 `R.ap`로 적용할 함수를 인자로 계속 추가할 수 있다.
- `('Ramda')` 함수가 아닌 대상을 인자로 넣게 되면 미리 `R.ap`의 인자로 받아온 함수를 `R.concat` `R.toUpper`를 각각 적용한다.
- `R.concat` 함수에 `'Ramda'`를 문자열을 넣게 되면 새로운 문자열을 인자로 받아 `'Ramda새로운문자열'`이란 문자열을 반환하는 함수를 만든다.
- `R.toUpper`에 `'Ramda'` 문자열을 넣게 되면 `RAMDA`가 반환된다.
- 반환된 `RAMDA`를 `R.ap`의 이전 인자인 `R.concat` 함수의 인자로 넣은 결과인 `'RamdaRAMDA'`를 반환한다.

## Reference
- https://ramdajs.com/docs/#ap
