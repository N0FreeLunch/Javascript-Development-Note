# dropLast

> Returns a list containing all but the last n elements of the given list.
- 주어진 리스트에서 마지막 n개의 원소를 제외한 모든 것이 포함된 리스트를 반환한다.
> Acts as a transducer if a transformer is given in list position.
- 만약 리스트 위치에 변형기가 전달되었다면 변환기로서 작동한다.
> See also takeLast, [drop](./drop.md), [dropWhile](./dropWhile.md), [dropLastWhile](./dropWhile.md).

## 설명

- drop이 앞에서 부터 지정한 번째까지의 원소를 지운 것에 반해 dropLast는 뒤에서 부터 지정한 번째까지의 원소를 지운다.

## 문법

```
R.dropLast(Number: n, Array: list): Array
```
- `n`: The number of elements of list to skip.
- `n`: 건너뛸 리스트의 원소의 갯수 (여기서 skip이라는 것이 적절하지 않은 표현일 수 있다. skip이 아닌 제거할이라는 의미를 가진 것으로 사용해야 적당할 것 같다.)
- `list`: The list of elements to consider.
- `list`: 대상 원소들이 담긴 리스트
- Returns Array A copy of the list with only the first `list.length - n` elements
- 배열을 반환한다. 이 배열은 처음 (리스트애서) `list.length - n`개의 원소들을 갖는 리스트의 복사본이다.

## 표현

```
Number → [a] → [a]
```
- `Number →`: 첫 번째 인자 제거할 원소의 수를 입력 받는다.
- `→ [a] →`: 두 번째 인자로 대상 배열을 받는다. 이 때, 배열의 모든 원소는 동일한 종류여야 한다.
- `→ [a]`: 두 번째 인자로 받은 대상에서 첫 번째 인자로 받은 수 만큼 배열의 마지막에서 제거한 배열을 반환한다.

```
Number → String → String
```
- `Number →`: 첫 번째 인자로 제거할 문자의 수를 입력 받는다.
- `→ String →`: 두 번째 인자로 대상 문자열을 받는다.
- `→ String`: 두 번째 인자로 받은 문자열의 첫 번째 인자로 받은 수 만큼의 문자를 마지막 부터 제거한 문자열을 반환한다.

## 예제

```js
R.dropLast(1, ['foo', 'bar', 'baz']); //=> ['foo', 'bar']
R.dropLast(2, ['foo', 'bar', 'baz']); //=> ['foo']
R.dropLast(3, ['foo', 'bar', 'baz']); //=> []
R.dropLast(4, ['foo', 'bar', 'baz']); //=> []
R.dropLast(3, 'ramda');               //=> 'ra'
```

- `['foo', 'bar', 'baz']`의 복사본에서 뒤에서 1개의 원소 `'baz'`를 제거한 `['foo', 'bar']`를 반환한다.
- `['foo', 'bar', 'baz']`의 복사본에서 뒤에서 2개의 원소 `'bar', 'baz'`를 제거한 `['foo']`를 반환한다.
- `['foo', 'bar', 'baz']`의 복사본에서 뒤에서 3개의 원소 `'foo', 'bar', 'baz'`를 제거한 `[]`를 반환한다.
- `['foo', 'bar', 'baz']`의 복사본에서 뒤에서 4개의 원소를 제거하려고 했으나 3개의 원소 `'foo', 'bar', 'baz'`만 존재하므로 3개만 제거한 `[]`를 반환한다.
- `'ramda'`의 복사본에서 (문자열은 값이므로) 뒤에서 3개의 문자를 제거한 `'ra'`를 반환한다.

## References

- https://ramdajs.com/docs/#dropLast
- https://github.com/ramda/ramda/blob/master/test/dropLast.js
- https://github.com/ramda/types/blob/develop/types/dropLast.d.ts
