## mergeRight
> Create a new object with the own properties of the first object merged with the own properties of the second object.
- 첫 번째 오브젝트가 가진 프로퍼티들에 두 번째 오브젝트가 가진 프로퍼티를 통합한 새로운 오브젝트를 생성한다.
> If a key exists in both objects, the value from the second object will be used.
- 만약 키가 두 오브젝트 모두에 존재한다면, 해당 키의 값은 두 번째 오브젝트의 것을 사용한다.

> See also mergeLeft, mergeDeepRight, mergeWith, mergeWithKey.

## 설명
- `mergeLeft` 함수와 우선순위의 적용이 반대인 함수
- 주어진 두 오브젝트의 모든 인자를 가진 오브젝트를 생성한다. 단 두 오브젝트의 키가 중복되는 경우 두 번째로 받은 오브젝트의 키값을 적용한다.

## 표현
```
{k: v} → {k: v} → {k: v}
```
- `{k: v} → ` 첫 번째 인자로 키-벨류 형식으로 구성된 오브젝트를 받는다.
- `→ {k: v} →` 두 번째 인자로 키-벨류 형식으로 구성된 오브젝트를 받는다.
- `→ {k: v}` 두 오브젝트의 모든 키-벨류를 가진 새로운 오브젝트를 반환한다. 이 때 키의 중복이 있다면 두 번째 오브젝트의 키 값을 적용한다.

## 예제
```
R.mergeRight({ 'name': 'fred', 'age': 10 }, { 'age': 40 });
//=> { 'name': 'fred', 'age': 40 }

const withDefaults = R.mergeRight({x: 0, y: 0});
withDefaults({y: 2}); //=> {x: 0, y: 2}
```
- `R.mergeRight({x: 0, y: 0})`는 오브젝트를 하나 더 인자로 받아서 기본적으로 세팅된 오브젝트 `{x: 0, y: 0}` 값에 추가 변경할 키-벨류 쌍을 정의한 오브젝트를 추가하여 오브젝트를 뽑아낼 수 있는 기능을 제공하는 것이 `withDefaults`함수이다. 기본 오브젝트에 `{y: 2}`란 오브젝트를 추가하여 기존 `y`키 값을 `2`로 바꾸었다.

## Reference
- https://ramdajs.com/docs/#mergeRight
