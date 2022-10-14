## last
> Returns the last element of the given list or string.
- 주어진 리스트 또는 문자열의 마지막 원소를 반환한다.

## 표현
```
[a] → a | Undefined
String → String
```

## 설명
- 주어진 배열의 마지막 원소를 반환하며 반환할 원소가 없다면 undefined를 반환한다.
- 배열이 아닌 문자열이 주어진 경우 마지막 문자를 반환하며 마지막 문자가 없다면 빈 문자열 `''`을 반환한다.

## 예제
```
R.last(['fi', 'fo', 'fum']); //=> 'fum'
R.last([]); //=> undefined

R.last('abc'); //=> 'c'
R.last(''); //=> ''
```
- 배열 `['fi', 'fo', 'fum']`를 받아서 마지막 원소를 반환하므로 `'fum'`를 반환한다.
- 배열 `[]`를 받아서 마지막 원소를 반환해야 하는데 마지막 원소가 없으므로 undefined를 반환한다.
- 문자열 `'abc'`를 받아서 마지막 문자를 반환하므로 `'c'`를 반환한다.
- 문자열 `''`를 받아서 마지막 문자를 반환해야하는데 마지막 문자가 없으므로 `''`를 반환한다.

## Reference
- https://ramdajs.com/docs/#last
