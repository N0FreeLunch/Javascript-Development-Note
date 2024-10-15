## ap

> ap applies a list of functions to a list of values.
- 값을 나열한 리스트를 받아서 함수를 원소로 하는 리스트를 적용한다.

> Dispatches to the ap method of the second argument, if present. Also treats curried functions as applicatives.

## 설명

- applies 라는 뜻을 가진 함수이다.
- 먼저 인자를 넣었을 때 반환 되는 구조를 입력하고 구조의 일부에 해당하는 인자를 넣었을 때, 설정된 구조에 따라서 결과를 반환하는 함수이다.
- 함수 리스트와 값 리스트를 받아서 값 리스트의 대상을 함수 리스트 각각에 전달하여 얻은 결과를 모두 합친 배열을 반환한다.

## 표현

### 배열을 인자로 사용할 때
```
[a → b] → [a] → [b]
```
- `a → b` `a` 타입의 값을 받았을 때 `b`라는 타입의 값을 반환하는 함수이다.
- `[a → b] →`는 `a → b` 함수를 단일 또는 여러 개 배열에 넣은 것을 인자로 받는다는 의미이다. 이때 여러 다른 함수를 배열의 원소로 받을 수 있지만, `a → b`로 되어 있는 것은 타입 `a`를 넣었을 때 타입 `b`를 반환하는 함수를 배열의 원소로 넣어야 한다.
- ` → [a]` 다음 인자로 `[a]`로 적용할 대상 값들의 집합인 배열을 인자로 받는다.
- `[a → b]`에서 설정한 `a → b` 구조에 따라서 타입 a를 원소로 한 `[a]`를 인자로 집어 넣었을 때 타입 b를 원소로 한 `[b]`를 반환한다.
- `→ [b]` 결과값을 배열 형태로 반환한다.

### 커링된 함수를 인자로 사용할 때
```
Apply f => f (a → b) → f a → f b
```
- `Apply f => ` `f`는 fantasy-land의 [apply](https://github.com/fantasyland/fantasy-land?tab=readme-ov-file#apply)의 사양을 만족하는 대상이다.
- `Apply f`는 `R.ap()` 함수의 첫번째 인자로 커링된 함수를 받는다는 의미이다.
- `=> f (a → b)`는 인자를 하나 받으면 평가될 수 있는 함수인 `a -> b`를 인자로 받는 함수로 `R.ap()`의 첫 번째로 받은 함수 f에 두 번째로 받은 인자인 `a → b` 함수를 인자로 집어 넣는다.
- 이로 인해 반환된 함수는 설정된 `a → b` 규약에 따라 a를 내포한 함수 `f a`를 인자로 받았을 경우 b를 내포한 함수 f b`를 반환한다.

### ???
```
(r → a → b) → (r → a) → (r → b)
```
- `(r → a → b)`는 `r`이란 인자를 받고 다음으로 `a`란 인자를 받았을 때 `b`란 결과를 반환하는 함수이다.
- `(r → a)`는 `r`이란 인자를 `a`란 결과로 변경하는 함수를 인자로 받으면 앞서 설정된 `(r → a → b)`에 따라
- `→ (r → b)`에서 `r`이란 인자를 받았을 때 b라는 결과값을 반환하는 함수 `(r → b)`를 만든다는 의미

## 예제
```js
R.ap([R.multiply(2), R.add(3)], [1,2,3]); //=> [2, 4, 6, 4, 5, 6]
```
- `R.multiply(2)`는 수 하나를 원소로 받아 2를 곱하는 함수이다. `R.add(3)`은 수 하나를 원소를 받아 3을 더하는 함수이다.
- `R.ap([R.multiply(2), R.add(3)]);`에서 `[R.multiply(2), R.add(3)]` 배열 안의 함수를 두 번째 인자로 받는 `[1,2,3]`에 각각 적용한다.
- 두 번째 인자로 받는 배열의 각 원소가 함수의 인자가 되어 `R.multiply(2)(1)`, `R.multiply(2)(2)`, `R.multiply(2)(3)`을 한 결과 `[2,4,6]`을 얻는다. `R.add(3)(1)`, `R.add(3)(2)`, `R.add(3)(3)`한 결과 `[4,5,6]`을 얻는다. 해당 결과의 합집합인 `[2, 4, 6, 4, 5, 6]`이란 결과를 얻는다.

```js
R.ap([R.concat('tasty '), R.toUpper], ['pizza', 'salad']); //=> ["tasty pizza", "tasty salad", "PIZZA", "SALAD"]
```
- 배열을 첫번째 인자로 받기 때문에 두 번째 인자도 배열로 받는다.
- `R.concat('tasty ')`는 문자열 하나를 받아서 `tasty ` 문자열 뒤에 주어진 문자 원소를 받아서 반환하는 함수이다.
- `R.toUpper`는 주어진 문자열 하나를 받아서 소문자를 대문자로 바꾼다.
- `R.ap([R.concat('tasty '), R.toUpper], ['pizza', 'salad']);`에서 `R.concat('tasty ')`를 `['pizza', 'salad']`을 인자로 받아 `'tasty pizza'`, `'tasty salad'`를 만들어내고 `R.toUpper`를 `['pizza', 'salad']`에 적용하여 `"PIZZA"`, `"SALAD"`를 만들어 낸다. 해당 결과의 합집합인 `["tasty pizza", "tasty salad", "PIZZA", "SALAD"]`이란 결과를 얻는다.

```js
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
- https://www.youtube.com/watch?v=VGo_3EH17Ew
- https://github.com/ramda/ramda/blob/master/test/ap.js
- https://github.com/ramda/types/blob/develop/types/ap.d.ts
