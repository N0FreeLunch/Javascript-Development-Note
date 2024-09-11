## xor
> Exclusive disjunction logical operation. Returns true if one of the arguments is truthy and the other is falsy. Otherwise, it returns false.
- 베타적 선언의 논리 연산자이다. 만약 인자 중 하나가 truely 이고 다른 인자가 falsy라면 true를 반환하고 그렇지 않으면 false를 반환한다.

> See also [or](./or.md), [and](./and.md).

### 설명
- 두 인자를 받아 하나가 참으로 판단되고 하나가 거짓으로 판단되는 값일 때 true를 반환하고 그렇지 않으면 false를 반환한다.

### 표현
```
a → b → Boolean
```
- `a →`: 첫 번째 인자로 어떤 종류의 값을 받는다. 첫 번째 인자와 두 번째 인자는 참, 거짓의 판별이 가능한 종류의 truely 또는 falsy의 값이어야 한다.
- `→ b →`: 두 번째 인자로 어떤 종류의 값을 받는다. 첫 번째 인자와 다른 종류의 값을 받아도 상관없다.
- `→ Boolean`: 첫 번째 인자와 두 번째 인자가 서로  truely와 falsy로 달라질 때 true를 반환 아니면 false를 반환한다.

### 예제
```js
R.xor(true, true); //=> false
R.xor(true, false); //=> true
R.xor(false, true); //=> true
R.xor(false, false); //=> false
```
- true, true: 첫 번째 인자와 두 번째 인자가 서로 같은 진리값을 가지므로 false를 반환한다.
- true, false: 첫 번째 인자와 두 번째 인자가 서로 다른 진리값을 가지므로 true를 반환한다.
- false, true: 첫 번째 인자와 두 번째 인자가 서로 다른 진리값을 가지므로 true를 반환한다.
- false, false: 첫 번째 인자와 두 번째 인자가 서로 같은 진리값을 가지므로 false를 반환한다.

## References
- https://ramdajs.com/docs/#xor
