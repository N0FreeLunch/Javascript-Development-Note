## identical
> Returns true if its arguments are identical, false otherwise. Values are identical if they reference the same memory. NaN is identical to NaN; 0 and -0 are not identical.

> Note this is merely a curried version of ES6 Object.is.

## 표현
```
a → a → Boolean
```
- `a → ` 첫 번째 인자로 아무 값을 받는다.
- `→ a →` 두 번째 인자로 아무 값을 받는다.
- 첫 번째 인자와 두 번째 인자를 비교하여 같으면 참 아니면 거짓을 반환한다.

## 설명
- 주어진 두 인자가 일치하면 참을 반환하고 일치하지 않으면 거짓을 반환한다.
- 참조의 경우 참조하고 있는 원형이 같은지를 확인한다.
- 자바스크립트의 `==`이 자동 형 변환을 하여 비교하는 것과 형변환을 하지 않으며, `===`가 `+0 === -0`를 참으로 보는 것과 달리 거짓으로 본다는 점에서 여러 차이가 존재한다.
- 자바스크립트가 계산하는 값으로 존재하는 대상들 간의 비교가 아닌 인자로 넣었을 때의 값으로 존재하는 대상들간의 비교로 보면 될 듯하다.

## 예제
```
const o = {};
R.identical(o, o); //=> true
R.identical(1, 1); //=> true
R.identical(1, '1'); //=> false
R.identical([], []); //=> false
R.identical(0, -0); //=> false
R.identical(NaN, NaN); //=> true
```

## Reference
- https://ramdajs.com/docs/#identical
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/is
