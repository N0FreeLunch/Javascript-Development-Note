## mergeAll
> Creates one new object with the own properties from a list of objects. If a key exists in more than one object, the value from the last object it exists in will be used.
- 오브젝트로 이뤄진 리스트를 받아 각각의 오브젝트가 가진 프로퍼티들을 모두 합한 새로운 오브젝트를 만든다. 만약 오브젝트 간의 키의 중복이 있다면 주어진 리스트의 순서상 나중에 나열된 오브젝트의 벨류를 사용한다.
> See also reduce.

## 설명
- 여러개의 오브젝트를 통합해 하나로 만들기 위한 함수로, 여러 개의 오브젝트가 가진 각각의 키-벨류를 중복을 제외하고 모두 가진 오브젝트를 반환한다.
- 이 때 중복이 있을 경우 주어진 오브젝트 리스트의 순서상 나중에 위치한 오브젝트가 이전의 키-벨류를 덮어써서 유니크한 키가 반환된다.

## 표현
```
[{k: v}] → {k: v}
```
- `[{k: v}] →` 키-벨류로 이뤄진 오브젝트가 원소로 구성된 배열을 받는다.
- `→ {k: v}` 배열 안에 든 모든 오브젝트가 가진 키-벨류 쌍을 갖는 배열을 반환하며, 키의 중복이 있다면 배열에 나중에 나열된 키-벨류가 이전 키-벨류 쌍을 대체한다.

## 예시
```
R.mergeAll([{foo:1},{bar:2},{baz:3}]); //=> {foo:1,bar:2,baz:3}
R.mergeAll([{foo:1},{foo:2},{bar:2}]); //=> {foo:2,bar:2}
```
- `{foo:1}`에서 `foo` 값을, `{bar:2}`에서 `bar` 값을, `{baz:3}`에서 `baz`값을 가져와 오브젝트 `{foo:1,bar:2,baz:3}`를 만든다.
- `{foo:1}`에서 `foo` 값을 가져오지만 `{foo:2}`에서 `foo`키가 중복되기 때문에 `foo:1`을 버리고 나중에 나열된 `foo:2`를 가지며, `{bar:2}`에서 `baz`를 가져와 `{foo:2,bar:2}`를 만든다.

## Reference
- https://ramdajs.com/docs/#mergeAll
