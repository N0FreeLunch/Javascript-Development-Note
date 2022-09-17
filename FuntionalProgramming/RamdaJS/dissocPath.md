## dissocPath
> Makes a shallow clone of an object, omitting the property at the given path.
- 얕은 복사로 오브젝트를 복사한다. 복사된 오브젝트는 주어진 경로의 프로퍼티를 제외한다.
> Note that this copies and flattens prototype properties onto the new object as well.
- 얕은 복사는 새로운 오브젝트에도 프로토타입 프로퍼티를 복사하고 병합한다.
> All non-primitive properties are copied by reference.
- 모든 비 primitive 프로퍼티들은 참조로 복사된다.

## 표현
```
[Idx] → {k: v} → {k: v}
Idx = String | Int | Symbol
```
- `Idx = String | Int | Symbol` `Idx`는 문자열, 수, 심볼 타입이다. 
- `[Idx] →` 첫 번째 인자는 오브젝트에서 프로퍼티를 찾을 수 있는 인자를 지정한다.
- `→ {k: v} →` 두 번째 인자는 오브젝트를 지정한다.
- `→ {k: v}` 세 번째 인자는 두번째 오브젝트에서 첫번째 인자에서 지정한 프로퍼티를 제거한 오브젝트를 반환한다.

## 설명
- 첫 번째 인자로 프로퍼티를 찾을 수 있는 인자를 지정한다. 배열에 차례로 프로퍼티를 지정한다. 배열에 나열한 순서대로 프로퍼티에 할당된 오브젝트의 프로퍼티를 지정할 수 있다.
- 두 번째 인자로 오브젝트를 할당한다.
- 두 번째 인자의 오브젝트에서 첫 번째 인자에서 지정한 프로퍼티를 제거한 결과를 반환한다.

## 예제
```
R.dissocPath(['a', 'b', 'c'], {a: {b: {c: 42}}}); //=> {a: {b: {}}}
```
- `['a', 'b', 'c']` 대상 오브젝트의 프로퍼티 a에 접근하고 프로퍼티 a가 가지고 있는 오브젝트의 프로퍼티 b에 접근하고 프로퍼티 b가 가지고 있는 오브젝트의 프로퍼티 c에 접근하여 해당 프로퍼티를 삭제한다.
- `{a: {b: {c: 42}}}` 오브젝트에서 첫번째 인자에서 지정된 프로퍼티 `c: 42`를 제거한 결과 `{a: {b: {}}}`를 반환한다.

## Reference
- https://ramdajs.com/docs/#dissocPath
