## pickBy
> Returns a partial copy of an object containing only the keys that satisfy the supplied predicate.
- 오브젝트의 부분적인 복사본 반환한다. 반환되는 오브젝트는 주어진 술어함수를 만족하는 키만을 포함한다.

> See also pick, filter.

### 설명
- 오브젝트의 원소에서 키-벨류를 술어 함수에 넘겨 주었을 때 반환 값이 참이 되는 키-벨류 쌍만 결과 오브젝트로 반환한다.
- 첫 번째 인자로 파라메터의 순서가 벨류, 키를 인자로 받아 참/거짓을 반환하는 술어 함수를 받는다.
- 두 번째 인자로 대상 오브젝트를 받는다.
- 반환되는 결과는 두 번째 인자로 받는 오브젝트의 키-벨류 쌍에서 주어진 술어함수를 만족하는 키-벨류 쌍만을 가진 오브젝트이다.

### 표현
```
((v, k) → Boolean) → {k: v} → {k: v}
```
- `((v, k) → Boolean) →`: 첫 번째 인자로 키-벨류를 인자로 넘겨 받는 술어 함수를 받는다.
- `→ {k: v} →`: 두 번째 인자로는 오브젝트를 받는다.
- `→ {k: v}`: 반환돤 오브젝트 역시 키-벨류의 쌍을 갖지만, 두 번째 인자로 받은 오브젝트의 각각의 키-벨류 쌍에 대해 첫 번째 인자의 술어함수를 참으로 만드는 키-벨류 쌍만 들어있다.

### 예제
```js
const isUpperCase = (val, key) => key.toUpperCase() === key;
R.pickBy(isUpperCase, {a: 1, b: 2, A: 3, B: 4}); //=> {A: 3, B: 4}
```
- 술어 함수 `isUpperCase`는 오브젝트의 키가 대문자인지 확인하는 함수이다.
- `{a: 1, b: 2, A: 3, B: 4}`에 대해 오브젝트의 키가 대문자인 키-벨류 쌍은 `A: 3`과 `B: 4`이다. 따라서 결과 값은 `{A: 3, B: 4}`

## Reference
- https://ramdajs.com/docs/#pickBy
