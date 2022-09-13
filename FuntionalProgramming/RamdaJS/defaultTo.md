## defaultTo
> Returns the second argument if it is not null, undefined or NaN; otherwise the first argument is returned.
- 두 번째 인자가 null, undefined, NaN이 아닌 경우 두 번째 인자를 반환하고 그렇지 않으면 첫 번째 인자를 반환한다.

## 표현
```
a → b → a | b
```
- `a →` 디폴트로 출력할 값을 할당한다.
- `→ b →` 임의의 값 하나를 할당받아
- `→ a | b` 두번째 인자로 받은 값(`b`)이 정의되지 않은 값이면 디폴트 값인 a를 반환하고 받은 값이 정의된 값이면 b를 반환한다.

## 설명
- 인자로 정의되지 않은 값을 넣으면 디폴트 값을 반환하고, 정의된 값을 넣으면 정의된 값을 반환한다.
- 정의되지 않는 값의 유형은 null, undefined, NaN에 해당하는 값을 의미한다.

## 예제
```
const defaultTo42 = R.defaultTo(42);

defaultTo42(null);  //=> 42
defaultTo42(undefined);  //=> 42
defaultTo42(false);  //=> false
defaultTo42('Ramda');  //=> 'Ramda'
// parseInt('string') results in NaN
defaultTo42(parseInt('string')); //=> 42
```
- `null`은 정의되지 않은 값이므로 디폴트 값을 반환한다.
- `undefined`은 정의되지 않은 값이므로 디폴트 값을 반환한다.
- `false`는 정의된 boolean 값이므로 false를 반환한다.
- `'Ramda'`는 정의된 string 값이므로 'Ramda'를 반환한다.
- `NaN`은 정의되지 않은 값이므로 디폴트 값을 반환한다.

## Reference
- https://ramdajs.com/docs/#defaultTo
