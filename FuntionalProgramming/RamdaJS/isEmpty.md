## isEmpty
> Returns true if the given value is its type's empty value; false otherwise.
- 주어진 값이 값의 타입의 빈값이라면 참을 반환하고 아니면 거짓을 반환한다.

## 표현
```
a → Boolean
```
- `a →` 첫 번째 인자로 값을 받고
- `→ Boolean` 첫 번째 인자로 받은 값이 해당 값의 타입의 빈 값에 해당하면 참 아니면 거짓을 반환한다.

## 설명
- 어떤 값이 해당 값 타입의 빈값에 해당하는지 확인한다. 빈 값이면 참을 아니면 거짓을 반환한다.

## 예제
```
R.isEmpty([1, 2, 3]);           //=> false
R.isEmpty([]);                  //=> true
R.isEmpty('');                  //=> true
R.isEmpty(null);                //=> false
R.isEmpty({});                  //=> true
R.isEmpty({length: 0});         //=> false
R.isEmpty(Uint8Array.from('')); //=> true
```
- 배열의 빈 값은 `[]` 이므로 `R.isEmpty([1, 2, 3])`는 거짓이다.
- 배열의 빈 값은 `[]` 이므로 `R.isEmpty([])`는 참이다.
- 문자열의 빈 값은 `''`이므로 `R.isEmpty('')`는 참이다.
- null은 비어있는 타입이며 null 타입에서 비어있는 값이라고 할 수 없으므로 `R.isEmpty(null)`는 거짓이다.
- 오브젝트의 빈 값은 `{}`이므로 `R.isEmpty({})`는 참이다.
- 오브젝트의 빈 값은 `{}`이므로 `R.isEmpty({length: 0})`는 거짓이다.

## Reference
- https://ramdajs.com/docs/#isEmpty
