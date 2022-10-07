## intersperse
> Creates a new list with the separator interposed between elements.

> Dispatches to the intersperse method of the second argument, if present.

## 표현
```
a → [a] → [a]
```
- 첫 번째 인자로 임의의 종류의 어떤 값을 지정한다.
- 두 번째 인자로 임의의 종류의 값들이 나열된 배열을 받는다.
- 주어진 배열의 원소 사이사이에 첫 번째 인자를 원소로 넣은 배열을 반환한다.

## 설명
- 각 원소 사이에 지정한 원소를 넣는다. 원소와 원소 사이에만 넣기 대문에 첫 번째 인덱스와 마지막 인덱스에는 넣어지지 않는다.
- 첫 번째 인자로 배열에 넣을 원소를 지정한다.
- 두 번째 인자로 대상 배열을 지정한다.
- 주어진 배열의 모든 원소 사이사이에 첫 번째 인자의 원소를 끼워 넣은 결과를 반환한다.

## 예제
```
R.intersperse('a', ['b', 'n', 'n', 's']); //=> ['b', 'a', 'n', 'a', 'n', 'a', 's']
```
- `['b', 'n', 'n', 's']`애서 `'b', 'n'` 사이 `'n', 'n'` 사이 `'n', 's'` 사이에 `'a'`라는 원소를 넣는다. 따라서 결과는 `['b', 'a', 'n', 'a', 'n', 'a', 's']`이다.

## Reference
- https://ramdajs.com/docs/#intersperse
