## drop
> Returns all but the first n elements of the given list, string, or transducer/transformer (or object with a drop method).
> Dispatches to the drop method of the second argument, if present.

## 표현
```
Number → [a] → [a]
Number → String → String
```
- 첫 번째 인자로 몇 번째 인덱스까지 지울 것인지 정하는 수를 지정한다.
- 두 번째 인자로 배열을 넣을 경우 n번째 인덱스까지 지운 배열을 반환한다.

## 설명
- 첫 번째 인자로 배열의 몇 번째 인덱스까지 지울 것인지 정한다. 지정한 수가 배열의 길이를 초과할 경우 든 인덱스가 삭제되며 빈 배열이 반환된다.
- 두 번째 인자로 대상 배열을 지정한다. 배열이 아닌 문자열이 오면 문자열의 n번째 문자까지 지운 문자열을 반환한다. 

## 예제
```
R.drop(1, ['foo', 'bar', 'baz']); //=> ['bar', 'baz']
R.drop(2, ['foo', 'bar', 'baz']); //=> ['baz']
R.drop(3, ['foo', 'bar', 'baz']); //=> []
R.drop(4, ['foo', 'bar', 'baz']); //=> []
R.drop(3, 'ramda');               //=> 'da'
```
- 주어진 배열에서 첫 번째 인덱스까지의 원소를 제거한 결과를 반환한다. `['foo', 'bar', 'baz']`에서 첫번째 인덱스 `'foo'`를 제거하여 `['bar', 'baz']`가 된다.
- 주어진 배열에서 두 번째 인덱스까지의 원소를 제거한 결과를 반환한다. `['foo', 'bar', 'baz']`에서 두번째 인덱스까지 `'foo'`, `'bar'`를 제거하여 `['baz']`가 된다.

## Reference
- https://ramdajs.com/docs/#drop
