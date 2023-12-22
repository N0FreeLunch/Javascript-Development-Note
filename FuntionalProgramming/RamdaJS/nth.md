## nth
> Returns the nth element of the given list or string. If n is negative the element at index length + n is returned.
- 주어진 배열이나 문자열의 n번째 원소를 반환한다. 만약 n이 음수라면, 인덱스 길이 + n에 해당하는 원소가 반환된다.

## 설명

## 표현

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
