## eqProps
> Reports whether two objects have the same value, in R.equals terms, for the specified property. Useful as a curried predicate.

## 표현
```
k → {k: v} → {k: v} → Boolean
```
- `k →` 첫 번째 인자로 오브젝트의 키(k)를 받는다.
- `→ {k: v} → {k: v} → ` 두 번째와 세 번째 인자로 첫 번째 인자에서 지정한 키(k)가 들어 있는 오브젝트를 할당한다.
- `→ Boolean` 두 번째 인자와 세 번째 인자에서 첫 번째에 지정한 키의 벨류(v) 값이 같으면 참 아니면 거짓을 반환한다.

## 설명
- 첫 번째 인자로 대상 프로퍼티를 지정한다.
- 두 번째와 세 번째 인자로 오브젝트를 받는다.
- 두 번째와 세 번째 인자로 받은 오브젝트에서 첫 번째 인자에서 지정한 키의 값을 뽑아 일치하면 참 아니면 거짓을 반환

## 예제
```
const o1 = { a: 1, b: 2, c: 3, d: 4 };
const o2 = { a: 10, b: 20, c: 3, d: 40 };
R.eqProps('a', o1, o2); //=> false
R.eqProps('c', o1, o2); //=> true
```
- `o1`과 `o2`에서 프로퍼티 `'a'`를 선택하여 뽑아낸 값은 1, 10 이므로 일치하지 않아서 거짓
- `o1`과 `o2`에서 프로퍼티 `'c'`를 선택하여 뽑아낸 값은 3, 3 이므로 일치해서 참

## Reference
- https://ramdajs.com/docs/#eqProps
