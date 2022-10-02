## head
> Returns the first element of the given list or string. In some libraries this function is named first.
- 주어진 문자열 또는 리스트에서 첫 번째 원소를 반환한다. 일부 라이브러리에서 이 함수는 `first`라고 명명되어 있다.

## 표현
```
[a] → a | Undefined
String → String
```
- `[a] →` 첫 번째 인자로 배열을받는다. 배열의 원소는 어떤 종류의 값이든 가능하므로 `a`를 사용하여 표기하였다.
- `→ a | Undefined` 주어진 배열에서 첫 번째 원소를 반환하며 첫 번째 원소가 없으면 `undefined`를 반환한다. 하지만 문자열의 경우에는 undefined가 아닌 빈 문자열이 반환된다.

## 설명
- 배열의 첫 번째 원소 또는 유사 배열인 문자열의 첫 번째 원소인 첫 번째 문자를 반환한다.
- 배열의 경우 첫 번째 원소가 없는 경우 undefined가 반환되며, 문자열의 경우 빈문자열을 반환한다.

## 예제
```
R.head(['fi', 'fo', 'fum']); //=> 'fi'
R.head([]); //=> undefined

R.head('abc'); //=> 'a'
R.head(''); //=> ''
```

## Reference
- https://ramdajs.com/docs/#head
