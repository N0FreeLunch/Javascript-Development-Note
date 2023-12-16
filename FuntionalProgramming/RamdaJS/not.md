## not
> A function that returns the ! of its argument. It will return true when passed false-y value, and false when passed a truth-y one.
- 함수의 인자로 받은 값에 불리언 부정 기호 `!`를 사용한 결과를 반환한다. falsy-y에 해당하는 값을 인자로 전달 받았을 때 true를 반환하며 truth-y를 인자로 받았을 때는 false를 반환한다.

## 설명
- 하나의 인자를 받아서 해당 인자를 불리언으로 형변환 한 값의 논리 부정값을 반환한다.

## 표현
```
* → Boolean
```
- `* →` 임의의 인자를 하나 받는다.
- `→ Boolean` 받은 인자의 `!` 연산을 한 결과를 받으므로 `boolean` 타입을 반환한다.

## 예제
```js
R.not(true); //=> false
R.not(false); //=> true
R.not(0); //=> true
R.not(1); //=> false
```
- `R.not(true)`는 인자를 `true`를 받았으므로 `!true`에 해당하는 `false`를 반환한다.
- `R.not(false)`는 인자를 `false`를 받았으므로 `!false`에 해당하는 `true`를 반환한다.
- `R.not(0)`는 인자를 `0`를 받았으므로 `!0`에 해당하는 `true`를 반환한다.
- `R.not(1)`는 인자를 `1`를 받았으므로 `!1`에 해당하는 `false`를 반환한다.

## Refernce
- https://ramdajs.com/docs/#not
