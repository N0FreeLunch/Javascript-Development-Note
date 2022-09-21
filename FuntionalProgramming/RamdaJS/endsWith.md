## endsWith
> Checks if a list ends with the provided sublist.

> Similarly, checks if a string ends with the provided substring.

## 표현
```
[a] → [a] → Boolean
String → String → Boolean
```
- `[a] →` `String →` 첫 번째 인자로 배열 상당의 인자를 받는다.
- `→ [a] →` `→ String →` 두 번째 인자로 배열 상당의 인자를 받는다.
- 첫 번째 배열이 두 번째 배열의 부분집합이고 두 번째 배열의 마지막 부분에 위치하는 인자인 경우 참을 아니면 거짓을 반환한다.

## 설명
- 첫 번째 배열 또는 배열 형식의 리스트의 원소가 두 번째 배열의 마지막에 위치하는 원소 또는 원소들에 해당하는지 확인하여 속해 있으면 참 속해있지 않으면 거짓을 반환한다.

## 예제
```
R.endsWith('c', 'abc')                //=> true
R.endsWith('b', 'abc')                //=> false
R.endsWith(['c'], ['a', 'b', 'c'])    //=> true
R.endsWith(['b'], ['a', 'b', 'c'])    //=> false
```
- `'c'` `c`라는 원소는 배열 형식의 리스트인 문자열 `'abc'`의 마지막 원소에 해당하므로 참을 반환
- `'b'` `b`라는 원소는 배열 형식의 리스트인 문자열 `'abc'`의 마지막 원소에 해당하지 않으므로 거짓을 반환
- 문자열 `'c'`라는 원소는 배열의 마지막 원소 `'c'`와 일치하므로 참을 반환
- 문자열 `'b'`라는 원소는 배열의 마지막 원소 `'c'`와 일치하지 않으므로 거짓을 반환

## Reference
- https://ramdajs.com/docs/#endsWith
