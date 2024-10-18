## F
> A function that always returns false. Any passed in parameters are ignored
- 항상 거짓을 반환하는 함수이다. 파라메터로 전달된 어느 것도 무시된다.

> See also [T](./T.md).

### 설명
- 어떠한 인자를 넣든지 항상 fasle를 반환하는 함수

### 문법
```
R.F(Any): Boolean
```
- Returns Boolean

### 표현
```
* → Boolean
```
- `* →`: 임의의 인자를 받는다.
- `→ Boolean`: 항상 false를 반환한다.

### 예제
```
R.F(); //=> false
```
- `R.F()`는 항상 불리언 타입의 `false`를 반환한다.

## Referneces
- https://ramdajs.com/docs/#F
- https://github.com/ramda/ramda/blob/master/test/F.js
- https://github.com/ramda/types/blob/develop/types/F.d.ts
