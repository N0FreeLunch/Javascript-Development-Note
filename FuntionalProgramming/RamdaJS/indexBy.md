## indexBy
> Given a function that generates a key, turns a list of objects into an object indexing the objects by the given key.
- 키를 생성하는 함수를 하나 받아서, 원소가 오브젝트인 리스트를 함수에 인자로 전달되어 받은 결과로 얻은 키로 인덱싱을 한 오브젝트로 변환한다.

> Note that if multiple objects generate the same value for the indexing key only the last value will be included in the generated object.
- 만약 여러 오브젝트가 동일한 인덱싱 키를 생성한다면, 가장 마지막의 값이 생성된 오브젝트에 포함되어 버린다.

> Acts as a transducer if a transformer is given in list position.

## 표현
```
Idx a => (b → a) → [b] → {a: b}
Idx = String | Int | Symbol
```
- `Idx = String | Int | Symbol` Idx 종류는 오브젝트의 프로퍼티명으로 지정할 수 있는 종류의 타입이다.
- `Idx a =>` Idx 종류의 타입을 a라고 할 때
- `(b → a) →` 첫 번째 인자로 인자를 하나 받아서 Idx 종류의 타입의 값을 반환하는 함수를 받는다.
- `→ [b] →` 두 번째 인자로 첫 번째 인자의 함수의 인자로 전달할 수 있는 값을 원소로 하는 배열을 받는다.
- `→ {a: b}` 두 번째 인자로 받은 배열의 원소를 순차적으로 첫 번째 인자로 받은 함수의 인자로 전달하여 평가된 값을 키로 전달된 인자(배열의 원소)를 값으로 하는 오브젝트를 반환한다.

## 설명
- 주어진 배열의 원소를 주어진 함수에 전달하여 평가된 결과를 키로 전달 받은 인자를 값으로 하는 오브젝트를 반환한다.
- 오브젝트의 키는 하나이므로 함수의 리턴 값으로 이전과 동일한 키를 가진다면 가장 마지막에 키를 생성한 값을 키의 벨류가 된다.

## 예제
```
const list = [{id: 'xyz', title: 'A'}, {id: 'abc', title: 'B'}];
R.indexBy(R.prop('id'), list);
//=> {abc: {id: 'abc', title: 'B'}, xyz: {id: 'xyz', title: 'A'}}
```
- `R.prop('id')` 오브젝트를 인자로 받아서 오브젝트 내의 `id` 프로퍼티의 값을 반환한다. 곧 `id`프로퍼티의 값이 키가 된다.
- `R.indexBy(R.prop('id'), list)`는 리스트인 `[{id: 'xyz', title: 'A'}, {id: 'abc', title: 'B'}]`의 원소를 하나씩 받아서 `R.prop('id')` 함수의 인자로 전달한다.
- `{id: 'xyz', title: 'A'}`를 전달하면 키는 `'xyz'`가 되고 `{id: 'abc', title: 'B'}`를 전달하면 키는 `'abc'`가 된다.
- 따라서 반환 되는 오브젝트는 `xyz`를 키로 `{id: 'xyz', title: 'A'}`를 벨류로 하며, `abc`를 키로 `{id: 'abc', title: 'B'}`를 벨류로 하는 오브젝트를 반환한다.
- 반환되는 오브젝트의 키는 키의 순서대로 나열되므로 xyz 보다 `abc`가 먼저 반환되어 `{abc: {id: 'abc', title: 'B'}, xyz: {id: 'xyz', title: 'A'}}`가 된다.



## Reference
- https://ramdajs.com/docs/#indexBy
