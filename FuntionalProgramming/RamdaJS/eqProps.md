## eqProps
> Reports whether two objects have the same value, in R.equals terms, for the specified property. Useful as a curried predicate.
- 특정 프로퍼티에 대해 R.equals의 정의에 따라 두 오브젝트가 동일한 값을 가졌는지 보고한다. (두 오브젝트의 특정 프로퍼티를 비교하는) 커링된 술어함수로 유용하다.

## 설명
- 두 오브젝트의 특정 프로퍼티가 일치하는지 R.equals으로 같은지 판별한 결과를 얻는다.
- 첫 번째 인자로 대상 프로퍼티를 지정한다.
- 두 번째와 세 번째 인자로 오브젝트를 받는다.
- 두 번째와 세 번째 인자로 받은 오브젝트에서 첫 번째 인자에서 지정한 키의 값을 뽑아 일치하면 참 아니면 거짓을 반환한다.

## 문법

```
R.eqProps(prop, obj1, obj2): Boolean
```
> `prop`: The name of the property to compare
- `prop`: 비교할 프로퍼티의 이름
> `obj1`
- `obj1`: 첫 번째 오브젝트
> `obj2`
- `obj2`: 두 번째 오브젝트
> Returns Boolean
- Boolean을 반환한다.

## 표현
```
k → {k: v} → {k: v} → Boolean
```
- `k →`: 첫 번째 인자로 오브젝트의 키(k)를 받는다.
- `→ {k: v} → {k: v} → `: 두 번째와 세 번째 인자로 첫 번째 인자에서 지정한 키(k)가 들어 있는 오브젝트를 할당한다.
- `→ Boolean`: 두 번째 인자와 세 번째 인자에서 첫 번째에 지정한 키의 벨류(v) 값이 같으면 참 아니면 거짓을 반환한다.

## 예제

```js
const o1 = { a: 1, b: 2, c: 3, d: 4 };
const o2 = { a: 10, b: 20, c: 3, d: 40 };
R.eqProps('a', o1, o2); //=> false
R.eqProps('c', o1, o2); //=> true
```
- `o1`과 `o2`에서 프로퍼티 `'a'`를 선택하여 뽑아낸 값은 1, 10 이므로 일치하지 않아서 거짓
- `o1`과 `o2`에서 프로퍼티 `'c'`를 선택하여 뽑아낸 값은 3, 3 이므로 일치해서 참

## Reference
- https://ramdajs.com/docs/#eqProps
- https://github.com/ramda/ramda/blob/master/test/eqProps.js
- https://github.com/ramda/types/blob/develop/types/eqProps.d.ts
