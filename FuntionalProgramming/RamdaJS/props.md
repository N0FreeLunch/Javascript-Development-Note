## props
> Acts as multiple prop: array of keys in, array of values out. Preserves order.
- prop를 여럿 사용한 것과 같은 기능을 가진다. 오브젝트에 속한 키를 지정하면 키에 대응되는 값을 나열한 배열을 반환한다. 반환 되는 값은 주어진 키의 순서에 맞게 반환된다.

> See also prop, pluck, project.

### 설명
- 나열된 키의 순서에 맞게 오브젝트에서 키의 값을 추출하여 나열한다.
- 첫 번재 인자로 오브젝트에서 대상이 되는 프로퍼티의 리스트를 지정한다.
- 두 번째 인자로 대상 오브젝트를 지정한다.
- 지정한 프로퍼티의 값을 오브젝트에서 추출하여 주어진 키의 순서대로 대응되는 값을 나열한 배열을 반환한다.

### 표현
```
[k] → {k: v} → [v]
```
- `[k] →`: 키(k)를 원소로 하는 배열을 받는다.
- `→ {k: v} →`: 키(k)-벨류(v) 쌍이 들어 있는 오브젝트를 받는다.
- `→ [v]`: 첫 번째 인자의 키 리스트에 대응되는 값의 리스트를 반환한다.

### 예제
```js
R.props(['x', 'y'], {x: 1, y: 2}); //=> [1, 2]
R.props(['c', 'a', 'b'], {b: 2, a: 1}); //=> [undefined, 1, 2]

const fullName = R.compose(R.join(' '), R.props(['first', 'last']));
fullName({last: 'Bullet-Tooth', age: 33, first: 'Tony'}); //=> 'Tony Bullet-Tooth'
```
- `['x', 'y']` 추출할 키 리스트를 지정한다. `{x: 1, y: 2}`에서 x 프로퍼티에 해당하는 값인 1, y 프로퍼티에 해당하는 값인 2를 주어진 키의 순서 대로 나열한 배열 `[1,2]`를 반환한다.
- `{b: 2, a: 1}`에서 c는 존재하지 않으므로 undefined, a는 프로퍼티는 그 값이 1, b 프로퍼티는 그 값이 2이다. 따라서 키가 나열된 순서대로 값을 나열하면 `[undefined, 1, 2]`가 된다.

## Reference
- https://ramdajs.com/docs/#props
