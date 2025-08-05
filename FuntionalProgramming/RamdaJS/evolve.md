## evolve
> Creates a new object by recursively evolving a shallow copy of object, according to the transformation functions.

> All non-primitive properties are copied by reference.

> A transformation function will not be invoked if its corresponding key does not exist in the evolved object.

## 설명

- 첫 번째 인자로 프로퍼티의 값을 변환할 함수를 정의한 오브젝트를 받는다.
- 두 번째 인자로 오브젝트를 받는다.
- 첫 번째 인자에 지정한 오브젝트가 가진 프로퍼티와 동일한 키를 가진 프로퍼티가 두 번째 오브젝트에 있다면 첫 번째 인자의 오브젝트의 동일한 키의 프로퍼티에 할당된 함수의 인자에 값을 넣고 평가된 결과 값을 해당 프로퍼티의 벨류로 갖는 오브젝트를 반환한다.
- 첫 번째 안자로 받은 오브젝트의 프로퍼티의 벨류가 오브젝트인 경우 해당 오브젝트의 내부의 프로퍼티에 변환할 함수를 정의하고 두 번째 인자로 반든 오브젝트에서 동일한 프로퍼티의 프로퍼티에 할당된 벨류를 변환할 함수의 인자로 할당하여 평가된 결과 값을 넣어 반환된다. 같은 방식으로 중첩된 오브젝트에 계속 적용된다.

## 문법
```
R.evolve(transformations, object): Object
```
> `transformations`: The object specifying transformation functions to apply to the object.
- `transformations`: 
> `object`: The object to be transformed.
- `object`: 
> Returns Object The transformed object.
- 

## 표현

```
{k: (v → v)} → {k: v} → {k: v}
```
- `{k: (v → v)} →`: 첫 번째 인자로 키에 `(v → v)` 벨류(v)를 넣었을 때 동일 타입의 결과를 반환하는 함수를 할당
- `→ {k: v} → `: 두 번째 인자로 첫 번째 인자의 키를 가진 오브젝트를 할당
- `→ {k: v}`: 첫 번째 인자에 할당된 함수 `(v → v)`에 의해 프로퍼티가 변환된 벨류를 갖는 오브젝트를 반환

## 예제

```js
const tomato = {firstName: '  Tomato ', data: {elapsed: 100, remaining: 1400}, id:123};
const transformations = {
  firstName: R.trim,
  lastName: R.trim, // Will not get invoked.
  data: {elapsed: R.add(1), remaining: R.add(-1)}
};
R.evolve(transformations, tomato); //=> {firstName: 'Tomato', data: {elapsed: 101, remaining: 1399}, id:123}
```
- `transformations`를 보면 `firstName` 프로퍼티의 벨류는 `R.trim` 함수로 변경하고 `lastName` 프로퍼티의 벨류는 `R.trim` 함수로 으로 변경하고 `data` 프로퍼티에 할당된 오브젝트의 `elapsed` 프로퍼티는 `R.add(1)` 으로 변경하고 `remaining` 프로퍼티는 `R.add(-1)`으로 변경한다.
- `tomato`의 `firstName` 프로퍼티는 `R.trim('  Tomato ')`의 결과 변환되고, `lastName` 프로퍼티는 없으므로 변환 대상이 아니며, data 프로퍼티 내부의 오브젝트의 `elapsed` 프로퍼티는 `R.add(1)(100)`의 결과로 변환되고 `remaining` 프로퍼티는 `R.add(-1)(100)`의 결과로 변환된다.

## References
- https://ramdajs.com/docs/#evolve
- https://github.com/ramda/ramda/blob/master/test/evolve.js
- https://github.com/ramda/types/blob/develop/types/evolve.d.ts
