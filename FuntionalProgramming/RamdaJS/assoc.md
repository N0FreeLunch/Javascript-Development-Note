## assoc
- R.assoc()
> Makes a shallow clone of an object
- 오브젝트를 복사하며 얕은 복사를 한다.
> setting or overriding the specified property with the given value.
- 프로퍼티와 값을 새롭게 세팅 하거나 기존 프로퍼티의 값을 오버라이딩 한다.
> Note that this copies and flattens prototype properties onto the new object as well.
- 반환되는 새 오브젝트에는 프로토타입 프로퍼티도 복사 되고 병합(flattens)된다.
> All non-primitive properties are copied by reference.
- 프리미티브 타입이 아닌 값을 가지는 프로퍼티는 참조 방식으로 복사된다. (주소가 복사되고 실제 할당된 값이 복사되지 않는다.)



## 표현
```
Idx → a → {k: v} → {k: v}
Idx = String | Int
```
- `Idx →` Idx(인덱스) 곧, 프로퍼티명을 받는다.
- `→ a` 프로퍼티의 값을 받는다.
- `→ {k: v} →` 오브젝트를 받아서
- `→ {k: v}` 오브젝트를 반환한다. 이때 반환 된 오브젝트는 `→ {k: v} →`의 오브젝트에서 프로퍼티의 키 벨류 값이 들어간 값을 받는다.
- `Idx = String | Int` Idx로 가능한 타입은 문자열과 정수타입이다.

## 설명
```
R.assoc(프로퍼티명, '프로퍼티 값', 오브젝트)
```
- 첫 번째 인자로 프로퍼티명을 넣는다.
- 두 번째 인자로 프로퍼티 값을 넣는다.
- 세 번째 인자로 첫 번째 인자와 두 번째 인자로 받은 프로퍼티 이름과 값을 넣을 오브젝트를 할당한다.
- 세 번째 인자로 받은 오브젝트에 새로운 프로퍼티가 추가된 오브젝트를 반환한다.

## 예제
```
R.assoc('c', 3, {a: 1, b: 2}); //=> {a: 1, b: 2, c: 3}
```
- `{a: 1, b: 2}`라는 오브젝트에 `c: 3`를 넣은 오브젝트를 반환하여 `{a: 1, b: 2, c: 3}`가 된다.

## Reference
- https://ramdajs.com/docs/#assoc
