## whereEq
> Takes a spec object and a test object; returns true if the test satisfies the spec, false otherwise.
- 스펙 오브젝트와 테스트 오브젝트를 받는다. 만약 테스트 (오브젝트)가 스펙을 만족하면 true를 반환하며 그렇지 않으면 false를 반환한다.
> An object satisfies the spec if, for each of the spec's own properties, accessing that property of the object gives the same value (in R.equals terms) as accessing that property of the spec.
- 오브젝트가 스펙을 만족한다는 것은, 스펙 자체의 프로퍼티 각각에 대해 (테스트) 오브젝트의 프로퍼티에 접근했을 때(의 값과) 스펙의 프로퍼티에 접근할 때(의 값이) (R.equals 기준으로) 같은 값이 제공될 때이다.

> whereEq is a specialization of where.
- whereEq는 where을 (술어 함수가 아닌 프로퍼티의 일치를 조건으로 하는) 특수화 한 것이다.

> See also propEq, where.

### 설명
- 스펙 오브젝트와 테스트 오브젝트를 받아서 테스트 오브젝트의 (key, value) 쌍을 원소로 하는 집합의 부분집합이 스펙 오브젝트의 (key, value) 쌍을 원소로 하는 집합이 되는 경우, true를 반환하고, 그렇지 않으면 false를 반환한다.

### 표현
```
{String: *} → {String: *} → Boolean
```
- `{String: *} →`: 첫 번째 인자로는 오브젝트를 받는데, 스펙 오브젝트로 불린다. 이 오브젝트는 문자열의 프로퍼티를 가지고 프로퍼티가 어떤 값(`*`으로 종류에는 제한 없음)이어야 한다.
- `→ {String: *} →`: 두 번째 인자로는 오브젝트를 받는데, 테스트 오브젝트로 불린다. 이 오브젝트는 첫 번째 오브젝트의 프로퍼티와 일치할 수 있어야 하므로 문자열 프로퍼티를 가지며, 각 프로퍼티는 어떤 값(`*`으로 종류에는 제한 없음)을 가진다.
- `→ Boolean`: 테스트 오브젝트의 프로퍼티 중 일부가 스펙 오브젝트에 정의된 모든 동일한 프로퍼티의 값과 R.equals 함수를 기준으로 비교했을 때 일치하는 경우 true를 반환하고 그렇지 않으면 false를 반환한다.

### 예제
```js
// pred :: Object -> Boolean
const pred = R.whereEq({a: 1, b: 2});

pred({a: 1});              //=> false
pred({a: 1, b: 2});        //=> true
pred({a: 1, b: 2, c: 3});  //=> true
pred({a: 1, b: 1});        //=> false
```
- 주어진 스펙 오브젝트는 `{a: 1, b: 2}`이다. 테스트 오브젝트는 a 프로퍼티의 값이 1이고 b의 프로퍼티 값이 2이야 true가 반환되고 그렇지 않으면 false를 반환한다.
- `{a: 1}`는 b 프로퍼티가 undefined가 되므로 스펙을 만족하지 못한다. `{a: 1, b: 2}`는 스펙 오브젝트의 동일한 프로퍼티의 모든 값과 일치하기 때문에 스펙을 만족한다. `{a: 1, b: 2, c: 3}`는 스펙 오브젝트의 동일한 프로퍼티의 모든 값과 일치하기 때문에 스펙을 만족한다. `c: 3`은 스펙 오브젝트에 없기 떄문에 조건을 만족해야 할 대상은 아니다. `{a: 1, b: 1}`는 `b: 1`이 스펙 오브젝트와 일치하지 않기 때문에 스펙을 만족하지 않는다.

## References
- https://ramdajs.com/docs/#whereEq
