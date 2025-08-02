## endsWith

> Checks if a list ends with the provided sublist.
- 하나의 리스트의 맨 마지만이 주어진 서브 리스트로 이뤄져 있는지 있는지 확인한다.

> Similarly, checks if a string ends with the provided substring.
- 유사하게, 문자열의 마지막이 제공된 서브 문자열로 이뤄져 있는지 확인한다.

## 설명

- 첫 번째 배열이 두 번째 배열의 맨 마지막에 나열된 원소와 일치하는지 확인하여 참 또는 거짓을 반환한다.

## 문법

```
R.endsWith(suffix, list): Boolean
```
> suffix
> list
> Returns Boolean

## 표현

```
[a] → [a] → Boolean
String → String → Boolean
```
- `[a] →`, `String →`: 첫 번째 인자로 배열 상당의 인자를 받는다.
- `→ [a] →`, `→ String →`: 두 번째 인자로 배열 상당의 인자를 받는다.
- 첫 번째 배열이 두 번째 배열의 부분집합이고 두 번째 배열의 마지막 부분에 위치하는 인자인 경우 참을 아니면 거짓을 반환한다.

## 예제

```js
R.endsWith('c', 'abc')                //=> true
R.endsWith('b', 'abc')                //=> false
R.endsWith(['c'], ['a', 'b', 'c'])    //=> true
R.endsWith(['b'], ['a', 'b', 'c'])    //=> false
```
- `'c'` `c`라는 원소는 배열 형식의 리스트인 문자열 `'abc'`의 마지막 원소에 해당하므로 참을 반환
- `'b'` `b`라는 원소는 배열 형식의 리스트인 문자열 `'abc'`의 마지막 원소에 해당하지 않으므로 거짓을 반환
- 문자열 `'c'`라는 원소는 배열의 마지막 원소 `'c'`와 일치하므로 참을 반환
- 문자열 `'b'`라는 원소는 배열의 마지막 원소 `'c'`와 일치하지 않으므로 거짓을 반환

## References
- https://ramdajs.com/docs/#endsWith
- https://github.com/ramda/ramda/blob/master/test/endsWith.js
- https://github.com/ramda/types/blob/develop/types/endsWith.d.ts
