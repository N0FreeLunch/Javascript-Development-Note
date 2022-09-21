## equals
> Returns true if its arguments are equivalent, false otherwise. Handles cyclical data structures.

> Dispatches symmetrically to the equals methods of both arguments, if present.

## 표현
```
a → b → Boolean
```
- `a →` 첫 번째 인자를 받고
- `→ b →` 두 번째 인자를 받는데 두 번째 인자는 첫 번째 인자와 타입이 달라도 된다.
- `→ Boolean` 받은 두 인자의 값이 일치하면 참 아니면 거짓을 반환한다.

## 설명
- 두 인자를 받아서 타입과 값이 일치하면 참을 아니면 거짓을 반환한다.
- 인자가 오브젝트인 경우 두 오브젝트의 정의된 프로퍼티의 키와 벨류가 일치하면 동일하다고 판단한다. 이 때 벨류가 오브젝트인 경우도 키와 벨류가 일치하면 동일하다고 판단한다.

## 예제
```
R.equals(1, 1); //=> true
R.equals(1, '1'); //=> false
R.equals([1, 2, 3], [1, 2, 3]); //=> true

const a = {}; a.v = a;
const b = {}; b.v = b;
R.equals(a, b); //=> true
```
- `1, 1` 타입과 값이 같으므로 참을 반환
- `1, '1'` 타입이 다르므로 거짓을 반환
- `[1, 2, 3], [1, 2, 3]` 타입과 값이 같으므로 참을 반환
- `a = {}; a.v = a` `{}; b.v = b` 두 오브젝트의 프로퍼티 키가 `v`로 동일하고 벨류가 빈 오브젝트로 동일하므로 참을 반환

## Reference
- https://ramdajs.com/docs/#equals
