## defaultTo

> Returns the second argument if it is not null, undefined or NaN; otherwise the first argument is returned.
- 두 번째 인자가 null, undefined, NaN이 아닌 경우 두 번째 인자를 반환하고 그렇지 않으면 첫 번째 인자를 반환한다.

### 설명

- 무효한 값은 null, undefined, NaN 이라고 할 때, 인자로 무효한 값을 넣으면 디폴트 값을 반환하고, 정의된 값을 넣으면 정의된 값을 반환한다.

### 문법

```
R.defaultTo(default, val): *
```
> `default`: The default value.
- `default`: 기본값으로 사용할 값
> `val`: val will be returned instead of default unless val is null, undefined or NaN.
- `val`: val가 null, undefined, NaN이 아니라면 기본값 대신에 val을 반환한다.
> Returns * The second value if it is not `null`, `undefined` or `NaN`, otherwise the default value
- 임의의 종류(*)의 값을 반환한다. 이 값은 `null`, `undefined`, `NaN`이거나 그렇지 않으면 기본값을 반환한다.

### 표현

```
a → b → a | b
```
- `a →`: 디폴트로 출력할 값을 할당한다.
- `→ b →`: 임의의 값 하나를 할당받아
- `→ a | b`: 두번째 인자로 받은 값(종류는 `b`)이 무효한 값이면 디폴트 값(종류는 `a`)을 반환하고 유효한 값이라면 두 번째 값 그대로(종류는 `b`)를 반환한다.

### 예제

```js
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

## References
- https://ramdajs.com/docs/#defaultTo
- https://github.com/ramda/ramda/blob/master/test/defaultTo.js
- https://github.com/ramda/types/blob/develop/types/defaultTo.d.ts
