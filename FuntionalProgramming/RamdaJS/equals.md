## equals

> Returns true if its arguments are equivalent, false otherwise. Handles cyclical data structures.
- 인자들이 서로 동등하다면 true를 반환하고 그렇지 않으면 false를 반환한다. 순환하는 데이터 구조의 동등성도 다룰 수 있다.

> Dispatches symmetrically to the equals methods of both arguments, if present.
- 두 인자의 eqaul 메소드가 존재한다면 양쪽 모두의 equal 메소드를 실행하여 (한쪽의 메소드의 eqaul를 만족한다면 해당 메소드를 통해) 동일한지 확인한다.

## 설명

- 두 인자를 받아서 값이 일치하면 참을 아니면 거짓을 반환한다.
- 인자가 오브젝트인 경우 두 오브젝트의 정의된 프로퍼티의 키와 벨류가 일치하면 동일하다고 판단한다. 이 때 벨류가 오브젝트인 경우도 키와 벨류가 일치하면 동일하다고 판단한다.
- 각각의 인자에 equal 메소드가 존재한다면 이를 사용하여 동일한지 판단한다. Value Object를 사용한 동일성 판단을 할 수 있다.

## 문법

```
R.equal(a, b): Boolean
```
> `a`
- `a`: 일치를 비교할 대상
> `b`
- `b`: 첫 번째 인자와 일치하는지 확인할 대상
> Returns Boolean
- 일치하면 참, 일치하지 않으면 거짓

## 표현

```
a → b → Boolean
```
- `a →`: 첫 번째 인자로 임의의 값을 받는다.
- `→ b →`: 두 번째 인자도 임의의 값을 받는다. 첫 번째 인자와 두 번째 인자는 서로 타입이나 종류가 다른 인자여도 비교 가능하다. 물론 타입이 다를 경우에는 불일치로 처리된다.
- `→ Boolean`: 받은 두 인자의 값이 일치하면 참 아니면 거짓을 반환한다.

## 예제

```js
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

## References

- https://ramdajs.com/docs/#equals
- https://github.com/ramda/ramda/blob/master/test/equals.js
- https://github.com/ramda/types/blob/develop/types/equals.d.ts
