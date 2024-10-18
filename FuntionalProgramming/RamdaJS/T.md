## T
> A function that always returns true. Any passed in parameters are ignored.
- 항상 참을 반환하는 함수이다. 파라메터로 어떤 값을 전달해도 무시된다.

> See also [F](./F.md).

### 설명
- 인자를 하나 받아 인자의 값에 관계 없이 참을 반환한다. (단, `R.__`는 예외일 것)

### 문법
```
R.T(any): Boolean
```
- Returns Boolean

### 표현
```
* → Boolean
```
- `* →`: 임의의 인자를 하나 받는다.
- `→ Boolean`: 항상 true를 반환한다.

### 예제
```js
R.T(); //=> true
```

## Reference
- https://ramdajs.com/docs/#T
- https://github.com/ramda/ramda/blob/master/test/T.js
- https://github.com/ramda/types/blob/develop/types/T.d.ts
