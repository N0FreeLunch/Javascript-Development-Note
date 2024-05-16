## reject
> The complement of filter.
- filter의 차집합이다.

> Acts as a transducer if a transformer is given in list position.
- 만약 순회시 각각의 원소의 리스트 위치를 축적하는 transformer가 주어진다면, 순회 가능한 대상의 각각의 원소를 변환하는 transducer의 역할을 한다.

> Filterable objects include plain objects or any object that has a filter method such as Array.
- 필터할 수 있는 오브젝트는 plain objects 또는 배열과 같은 filter 메소드를 가진 오브젝트이다.

> See also filter, transduce, addIndex.

### 설명
- 배열이나 plan object와 같이 필터 가능한 오브젝트에 대해서, 주어진 술어함수를 만족하는 원소들은 기존 집합에서 제외한 차집합의 원소에 해당하는 대상만을 원소로 한 집합을 반환한다. 이 때 집합은 대상 오브젝트가 배열일 때는 배열의 형식으로 plan object인 경우에는 plan object의 형식으로 반환된다.

### 표현
```
Filterable f => (a → Boolean) → f a → f a
```
- `Filterable f =>`: 필터 가능한 오브젝트 f에 대해
- `(a → Boolean) →`: 첫 번째 인자로 술어 함수를 받는다.
- `→ f a →`: 두 번째 인자로 술어함수에 전달 가능한 요소 a를 가진 필터 가능한 오브젝트 f를 받는다.
- `→ f a`: 술어 함수를 통과한 요소만을 가진 오브젝트 f를 반환한다.

### 예제
```js
const isOdd = (n) => n % 2 !== 0;

R.reject(isOdd, [1, 2, 3, 4]); //=> [2, 4]

R.reject(isOdd, {a: 1, b: 2, c: 3, d: 4}); //=> {b: 2, d: 4}
```
- `isOdd`는 홀수인지 확인하는 술어 함수이며, `[1, 2, 3, 4]`, `{a: 1, b: 2, c: 3, d: 4}`는 필터 가능한 오브젝트이다.
- 술어함수를 통과하지 못하는 요소만을 가진 동일한 형태의 오브젝트를 반환하므로 `[1, 2, 3, 4]`는 배열인 `[2,4]`를, `{a: 1, b: 2, c: 3, d: 4}`는 오브젝트인 `{b: 2, d: 4}`를 반환한다.

## Reference
- https://ramdajs.com/docs/#reject
