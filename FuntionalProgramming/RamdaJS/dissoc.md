## dissoc

> Returns a new object that does not contain a prop property.
- 새로운 오브젝트를 반환한다. 이 오브젝트는 `prop` (파라메터에 인자로 전달하는) 프로퍼티를 포함하지 않는다.
> See also [assoc](./assoc.md), [omit](./omit.md).

## 설명

- 대상 오브젝트에서 주어진 프로퍼티를 제거한 오브젝트를 반환한다.

## 문법

```
R.dissoc(prop, obj): Object
```

> `prop`: The name of the property to dissociate
- `prop`: 제거할 프로퍼티의 이름 
> `obj`: The object to clone
- `obj`: 복사할 오브젝트
> Returns Object A new object equivalent to the original but without the specified property
- `Object`를 반환한다. 이 오브젝트는 특정한 프로퍼티만 가지지 않는 원본과 동등한 새로운 오브젝트를를 반환한다.

## 표현

```
String → {k: v} → {k: v}
```
- `String →`: 첫번째 인자로 제거할 프로퍼티 이름에 해당하는 문자열을 받는다.
- `→ {k: v} →`: 두 번째 인자로 대상 오브젝트를 받는다.
- `→ {k: v}`: 대상 오브젝트에서 지정한 프로퍼티 키를 제외한 오브젝트를 새로 만들어 반환한다.

## 예제

```js
R.dissoc('b', {a: 1, b: 2, c: 3}); //=> {a: 1, c: 3}
```
- `{a: 1, b: 2, c: 3}` 오브젝트에서 `'b'` 프로퍼티를 제거한 걸과를 반환하므로 `{a: 1, c: 3}`가 된다.

## References
- https://ramdajs.com/docs/#dissoc
- https://github.com/ramda/ramda/blob/master/test/dissoc.js
- https://github.com/ramda/types/blob/develop/types/dissoc.d.ts
