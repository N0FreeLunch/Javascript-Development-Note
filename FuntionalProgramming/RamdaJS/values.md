## values
> Returns a list of all the enumerable own properties of the supplied object.
- 주어진 오브젝트에서 열거 할 수 있는 자체 프로퍼티 모두의 리스트를 반환한다.
> Note that the order of the output array is not guaranteed across different JS platforms.
- 출력된 배열의 순서는 JS 플렛폼(브라우저 엔진, NodeJS, Bun, Deno 등)이 달라질 때 보장되지 않는다. 
> See also valuesIn, keys, toPairs.

### 설명
- 주어진 오브젝트에서 모든 프로퍼티의 키만 추출해서 배열에 담은 결과를 얻는다.
- 오브젝트의 자체(own) 프로퍼티만을 대상으로 하므로 프로토타입의 프로퍼티 등은 얻지 못한다.

### 표현
```
{k: v} → [v]
```
- `{k: v} →`: 첫 번째 인자로 오브젝트를 받는다.
- `→ [v]`: 오브젝트에서 키 정보는 제외하고 키의 값만을 나열한 배열을 얻는다. 따라서 오브젝트의 벨류가 가진 종류 v를 배열의 원소 종류로 한다.

### 예제
```js
R.values({a: 1, b: 2, c: 3}); //=> [1, 2, 3]
```
- `{a: 1, b: 2, c: 3}`에서 프로퍼티의 값 1,2,3만을 반환한다.

## References
- https://ramdajs.com/docs/#values
