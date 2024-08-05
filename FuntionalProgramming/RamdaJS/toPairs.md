## toPairs

> Converts an object into an array of key, value arrays.
- 오브젝트를 키, 벨류의 배열들로 변환한다.

> Only the object's own properties are used.
- 오브젝트가 갖고 있는 프로퍼티만을 사용해서 만든다.

> Note that the order of the output array is not guaranteed to be consistent across different JS platforms.
- 다양한 자바스크립트 플렛폼(각 브라우저의 자바스크립트 파싱 엔진)에서 출력되는 배열의 순서는 일관성이 보장되지 않는다. 

> See also fromPairs, keys, values.

### 설명
- 오브젝트의 키-벨류 쌍을 `[키, 벨류]` 형식의 배열을 나열한 배열의 형태로 바꾼다.

### 표현
```
{String: *} → [[String,*]]
```
- `{String: *} →`: 첫 번째 인자로는 문자열 키와 그에 대응하는 값을 갖는 오브젝트를 받는다.
- `→ [[String,*]]`: 오브젝트는 복수의 키를 가질 수 있으므로, `[문자열 키, 대응하는 값]`으로 변환한 배열을 원소로 하는 배열을 반환한다.

### 예제
```
R.toPairs({a: 1, b: 2, c: 3}); //=> [['a', 1], ['b', 2], ['c', 3]]
```
- 키-벨류 표기로 하면 a-1, b-2, c-3이 된다. [키, 벨류] 형식으로 나타내면 `['a', 1], ['b', 2], ['c', 3]`가 된다. 이를 나열한 배열은 `[['a', 1], ['b', 2], ['c', 3]]`가 된다.

## Reference
- https://ramdajs.com/docs/#toPairs
