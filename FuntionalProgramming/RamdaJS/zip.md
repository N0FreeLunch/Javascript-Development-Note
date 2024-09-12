## zip
> Creates a new list out of the two supplied by pairing up equally-positioned items from both lists.
- 두 리스트 양쪽에서 균일한 배치(equally-positioned)의 쌍을 만드는 것으로 새로운 리스트를 생성한다.
> The returned list is truncated to the length of the shorter of the two input lists.
- 반환된 리스트는 두 인풋 리스트 보다 더 짧은 길이(원소의 갯수)로 줄여져 있다.
> Note: zip is equivalent to zipWith(function(a, b) { return [a, b] }).
- 노트: zip은 `zipWith(function(a, b) { return [a, b] })`와 같다.

### 설명
- 두 배열을 받아 각 배열에서 동일한 인덱스의 값을 쌍으로 한 배열을 원소로 하는 배열을 반환한다.

### 표현
```
[a] → [b] → [[a,b]]
```
- `[a] →`: 첫 번째 인자로 배열을 받는다. 이 때 배열의 모든 원소는 동일한 종류여야 한다.
- `→ [b] →`: 두 번째 인자로 배열을 받는다. 이 때 배열의 모든 원소는 동일한 종류여야 한다. 하지만 첫 번째 인자로 받는 배열의 원소와는 다른 종류일 수 있다.
- `→ [[a,b]]`: 첫 번째 인자와 두 번째 인자로 받은 배열 양 쪽에서 동일한 인덱스의 값을 하나씩 취득하여 [첫 번째 배열에서 취득한 원소, 두 번째 배열에서 취득한 원소]의 쌍을 원소로 하는 배열을 생성한다.

### 예제
```js
R.zip([1, 2, 3], ['a', 'b', 'c']); //=> [[1, 'a'], [2, 'b'], [3, 'c']]
```
- 배열 `[1, 2, 3]`와 `['a', 'b', 'c']` 양쪽에서 같은 인덱스 번호 끼리 원소를 짝을 지어 원소를 만든다. 각 0번 인덱스에서 `[1, 'a']`을 각 1번 인덱스에서 `[2, 'b']`을 각 2번 인덱스에서 `[3, 'c']`의 쌍을 만들어 이를 담은 리스트를 반환한다. 따라서 `[[1, 'a'], [2, 'b'], [3, 'c']]`가 된다.

## References
- https://ramdajs.com/docs/#zip
