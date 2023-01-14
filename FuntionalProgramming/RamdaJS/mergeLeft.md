## mergeLeft
> Create a new object with the own properties of the first object merged with the own properties of the second object.
- 첫 번째 오브젝트가 가진 프로퍼티에 두 번째 오브젝트가 가진 프로퍼티들을 합친 새 오브젝트를 생성한다.
> If a key exists in both objects, the value from the first object will be used.
- 만약 동일한 키가 주어진 두 오브젝트 모두에 존재한다면, 해당 키의 값은 먼저 받은 오브젝트의 키값을 사용한다.

> See also mergeRight, mergeDeepLeft, mergeWith, mergeWithKey.

## 설명
- 두 개의 오브젝트를 받아서 각각의 오브젝트가 가진 키-벨류 세트를 모두 가진 새로운 오브젝트를 생성한다. 주어진 오브젝트 양쪽에 겹치는 키가 있다면 첫 번째 인자의 오브젝트의 프로퍼티를 사용한다.

## 표현
```
{k: v} → {k: v} → {k: v}
```
- `{k: v} →` 첫 번째 인자로 키-벨류 프로퍼티로 구성된 오브젝트를 받는다.
- `→ {k: v} →` 두 번째 인자로 키-벨류 프로퍼티로 구성된 오브젝트를 받는다.
- `→ {k: v}` 첫 번째와 두 번째 인자로 받은 키-벨류 쌍을 모두 가진 새로운 오브젝트를 반환한다. 단, 오브젝트이므로 키를 중복하지 않으며 키의 중복이 있다면 첫 번째 오브젝트를 반환한다.

## 예제
```
R.mergeLeft({ 'age': 40 }, { 'name': 'fred', 'age': 10 });
//=> { 'name': 'fred', 'age': 40 }

const resetToDefault = R.mergeLeft({x: 0});
resetToDefault({x: 5, y: 2}); //=> {x: 0, y: 2}
```
- `{ 'age': 40 }` `{ 'name': 'fred', 'age': 10 }` 두 오브젝트의 프로퍼티 중 키가 중복되는 것은 `age`이다. 첫 번째 인자로 받은 값을 우선하므로 반환되는 오브젝트에는 `'age': 40`이 들어가며, 각 오브젝트의 모든 프로퍼티를 키 중복을 단일화 한 모든 프로퍼티를 가진 오브젝트를 반환해야 하므로 `{ 'name': 'fred', 'age': 40 }`가 된다.
- `R.mergeLeft({x: 0})`라는 표현은 오브젝트를 하나 더 받아서 해당 오브젝트에 키 `x`가 없는 경우 `{x: 0}`을 넣고, `x`가 있는 경우 기존의 프로퍼티 대신에 `{x: 0}`를 바꾸는 역할을 한다. 곧 오브젝트에 무조건 `{x: 0}`란 프로퍼티를 추가하기 위한 함수가 `resetToDefault`이다.

## Reference
- https://ramdajs.com/docs/#mergeLeft
