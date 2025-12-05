# identical

> Returns true if its arguments are identical, false otherwise. Values are identical if they reference the same memory.
- (받는 두) 인자가 동일하면 true를 반환하며, 그렇지 않으면 false를 반환한다. 만약 같은 메모리를 참조한다면 값은 동일하다.
> NaN is identical to NaN; 0 and -0 are not identical.
- NaN은 NaN과 동일하며, 0 and -0는 동일하지 않다.

> Note this is merely a curried version of ES6 Object.is.
- 이것은 단지 ES6의 Object.is의 커링된 버전에 불과하다. [^1]

## 설명

- 자바스크립트 Object의 is 프로퍼티와 동일한 역할을 하는 것을 함수화 한 것으로 주어진 두 인자가 일치하는지 확인하는 함수이다.
- 두 값이 일치하면 참을 반환하고 일치하지 않으면 거짓을 반환한다. 값이 원본을 참조하고 있는 경우 참조하고 있는 원본이 같은지를 확인한다.
- 자바스크립트의 `==`이 자동 형 변환을 하여 비교하는 것과 형변환을 하지 않으며, `===`가 `+0 === -0`를 참으로 보는 것과 달리 거짓으로 본다는 점에서 차이점이 있다.
- 산술적 계산 관점에서는 일치하더라도, 자바스크립트로 표현되기로는 서로 다른 대상인 경우 다른 것으로 판정한다고 보면 된다.

## 문법

```
R.head(a, b): Boolean
```
> a
- a : 임의의 값
> b
- b : 임의의 값
> Returns Boolean
- Boolean 타입을 반환한다.

## 표현

```
a → a → Boolean
```
- `a → `: 첫 번째 인자로 아무 값을 받는다.
- `→ a →`: 두 번째 인자로 아무 값을 받는다.
- `→ Boolean`: 첫 번째 인자와 두 번째 인자를 비교하여 같으면 참 아니면 거짓을 반환한다.

## 예제

```js
const o = {};
R.identical(o, o); //=> true
R.identical(1, 1); //=> true
R.identical(1, '1'); //=> false
R.identical([], []); //=> false
R.identical(0, -0); //=> false
R.identical(NaN, NaN); //=> true
```

## References

- https://ramdajs.com/docs/#identical
- https://github.com/ramda/ramda/blob/master/test/identical.js
- https://github.com/ramda/types/blob/develop/types/identical.d.ts

[^1]: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/is
