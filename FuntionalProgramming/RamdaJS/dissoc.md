## dissoc
> Returns a new object that does not contain a prop property.

## 표현
```
String → {k: v} → {k: v}
```
- `String →` 첫번째 인자로 프로퍼티 이름에 해당하는 문자열을 받는다.
- `→ {k: v} →` 두 번째 인자로 대상 오브젝트를 받는다.
- `→ {k: v}` 대상 오브젝트에서 지정한 프로퍼티 키를 제외한 오브젝트를 새로 만들어 반환한다.

## 설명
- 대상 오브젝트에서 주어진 프로퍼티를 제거한 오브젝트를 반환한다.

## 예제
```
R.dissoc('b', {a: 1, b: 2, c: 3}); //=> {a: 1, c: 3}
```
- `{a: 1, b: 2, c: 3}` 오브젝트에서 `'b'` 프로퍼티를 제거한 걸과를 반환하므로 `{a: 1, c: 3}`가 된다.

## Reference
- https://ramdajs.com/docs/#dissoc
