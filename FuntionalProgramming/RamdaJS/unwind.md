## unwind
> Deconstructs an array field from the input documents to output a document for each element.
- 입력 문서에서 배열을 분리하여 각 원소에 대한 출력 문서를 생성한다.
> Each output document is the input document with the value of the array field replaced by the element.
- 각각의 출력 문서는 배열의 필드가 원소로 대체된 인풋 문서이다.

### 설명
- 대상 오브젝트에서 지정한 프로퍼티의 값이 배열인 경우, 지정한 프로퍼티의 값이 배열의 원소가 되도록 나머지 프로퍼티가 동일한 오브젝트를 만들고 지정한 프로퍼티의 값을 원본 배열의 원소로 구성한다.
- `{a: 1, b: [2, 3], c: 4}`라면 `[{a: 1, b: 2, c: 4}, {a: 1, b: 3, c: 4}]`를 하면 된다. b 프로퍼티를 지정했다면 b 프로퍼티의 배열을 나누어 b 프로퍼티가 1인 오브젝트와 2인 오브젝트 둘을 만든다.

### 표현
```
String → {k: [v]} → [{k: v}]
```
- `String →`: 첫 번째 인자로 대상 프로퍼티명을 지정한다.
- `→ {k: [v]} →`: 두 번째 인자로 오브젝트를 받는다. 이 때 오브젝트는 `{k: v|[v] }`의 표현이 되어야 하고, 첫 번째 인자에서 지정한 프로퍼티의 값이 배열인 경우 이 배열이 갖는 원소만큼 오브젝트를 생성한다.
- `→ [{k: v}]`: 생성된 오브젝트는 여럿이므로 배열에 오브젝트를 담은 값이 반환이 되며, 각각의 오브젝트에서 지정한 프로퍼티는 배열이 아닌 원본 오브젝트의 지정한 프로퍼티의 배열의 원소 값이 하나씩 들어가 있다.

### 예제
```js
R.unwind('hobbies', {
  name: 'alice',
  hobbies: ['Golf', 'Hacking'],
  colors: ['red', 'green'],
});
// [
//   { name: 'alice', hobbies: 'Golf', colors: ['red', 'green'] },
//   { name: 'alice', hobbies: 'Hacking', colors: ['red', 'green'] }
// ]
```
- `{ name: 'alice', hobbies: ['Golf', 'Hacking'], colors: ['red', 'green'], }`을 hobbies 프로퍼티는 배열로 구성되어 있다. hobbies 프로퍼티의 배열 원소를 분해하기 위해서 hobbies 프로퍼티가 `'Golf'`와 `'Hacking'`를 하나만 갖도록 하고 정보의 손실이 일어나지 않도록 하나의 오브젝트를 배열의 원소 갯수 만큼의 오브젝트로 분할한다. 따라서 `{ name: 'alice', hobbies: 'Golf', colors: ['red', 'green'] }`, `{ name: 'alice', hobbies: 'Hacking', colors: ['red', 'green'] }`가 된다.

## References
- https://ramdajs.com/docs/#unwind
