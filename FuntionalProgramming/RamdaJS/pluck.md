## pluck
> Returns a new list by plucking the same named property off all objects in the list supplied.
- 새로운 리스트를 반환한다. 주어진 리스트 내의 모든 오브젝트 각각에 대해 (지정한) 동일한 이름을 가진 프로퍼티를 뽑아낸다(pluck off).

> pluck will work on any functor in addition to arrays, as it is equivalent to R.map(R.prop(k), f).
- pluck은 R.map(R.prop(k), f)와 동치이므로 배열 외에도 모든 펑터에서 동작한다.

> See also project, prop, props.

### 설명

### 표현
```
Functor f => k → f {k: v} → f v
```
- `Functor f =>`: 펑터 f에 대해
- `k →`: 첫 번째 인자로는 오브젝트에서 뽑아낼 키(k)를 받는다. 각각의 오브젝트에서 추출할 프로퍼티 이름을 의미한다.
- `→ f {k: v} →`: 두 번째 인자로는 키-벨류 쌍의 오브젝트의 리스트(배열, 어떠한 유형의 펑터)를 받는다.
- `f v`: 추출한 값만을 가진 새로운 펑터를 생성한다.

### 예제
```js
var getAges = R.pluck('age');
getAges([{name: 'fred', age: 29}, {name: 'wilma', age: 27}]); //=> [29, 27]

R.pluck(0, [[1, 2], [3, 4]]);               //=> [1, 3]
R.pluck('val', {a: {val: 3}, b: {val: 5}}); //=> {a: 3, b: 5}
```

## Reference
- https://ramdajs.com/docs/#pluck
