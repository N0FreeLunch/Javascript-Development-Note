## nth
> Returns the nth element of the given list or string. If n is negative the element at index length + n is returned.
- 주어진 배열이나 문자열의 n번째 원소를 반환한다. 만약 n이 음수라면, 인덱스 길이 + n에 해당하는 원소가 반환된다.
- n이 음수일때, m을 n의 부호를 부정한 양수로 하자. 그러면 '인덱스 길이 + n'은 '인덱스 길이 + (-m)'과 같기 때문에 주어진 길이의 배열이나 문자열 내에서 원소를 선택할 수 있다.

## 설명
- 원하는 인덱스 번호에 해당하는 원소의 값을 반환한다. 음수 인덱스도 적용이 되며 음수 인덱스는 맨 뒤의 원소 부터 부터 -1, -2, -3의 인덱스가 차례로 적용된다.

## 표현
### 배열의 경우
```
Number → [a] → a | Undefined
```
- `Number →` 첫 번째 인자로 인덱스 번호를 받는다.
- `→ [a] → ` 두 번째 인자로 배열을 받는다.
- `→ a | Undefined` 지정한 인덱스에 해당하는 원소 또는 지정한 인덱스의 대상이 없는 경우 `undefined`를 반환한다.

### 문자열의 경우
```
Number → String → String
```
- `Number →` 첫 번째 인자로 인덱스 번호를 받는다.
- `→ String →` 두 번째 인자로 문자열을 받는다.
- `→ String` 선택된 인덱스 번호에 해당하는 문자를 반환한다. 문자는 한 글자의 문자열을 의미한다. 지정한 인덱스의 대상이 없는 경우 빈 문자열 `''`을 반환한다.

## 예제
```js
const list = ['foo', 'bar', 'baz', 'quux'];
R.nth(1, list); //=> 'bar'
R.nth(-1, list); //=> 'quux'
R.nth(-99, list); //=> undefined

R.nth(2, 'abc'); //=> 'c'
R.nth(3, 'abc'); //=> ''
```

### 배열의 경우
- `R.nth(1, list)`는 `list`에서 1번 인덱스에 해당하는 값 `'bar'`를 반환한다.
- `R.nth(-1, list)`는 `list`에서 -1번 인덱스에 해당하는 값, 뒤에서 첫 번째인 값인 `'quux'`를 반환한다.
- `R.nth(-99, list)`는 `list`에서 -99번 인덱스에 해당하는 값, 뒤에서 99번째인 값은 없으므로 `undefined`를 반환한다.

### 문자열의 경우
- `R.nth(2, 'abc')`는 `'abc'`에서 2번 인덱스에 해당하는 문자인 `'c'`를 꺼낸다.
- `R.nth(3, 'abc')`는 `''`에서 3번 인덱스에 해당하는 문자가 존재하지 않으므로 빈 문자열 `''`을 반환한다. 문자열의 경우 `undefined`가 아닌 빈 문자열을 반환한다.

## Reference
- https://ramdajs.com/docs/#nth
