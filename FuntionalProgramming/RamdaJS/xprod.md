## xprod
> Creates a new list out of the two supplied by creating each possible pair from the lists.
- 주어진 두 리스트로 부터 각각의 가능한 (모든) 쌍을 생성하는 것으로 새로운 리스트를 생성한다.

### 설명
- 두 리스트를 받아 각각의 리스트의 원소를 하나씩 원소 갖는 하는 '값의 쌍이 든 배열'을 원소로 하는 새로운 배열을 생성한다.
- 생성되는 리스트는 두 리스트에서 원소를 하나씩 뽑아 생성 가능한 모든 경우의 수의 쌍을 원소로 하는 리스트이다

### 표현
```
[a] → [b] → [[a,b]]
```
- `[a] →`: 첫 번째 인자로 배열을 받는다.
- `→ [b] →`: 두 번째 인자로 배열을 받는다.
- `→ [[a,b]]`: 첫 번째 인자와 두 번째 인자에서 원소를 하나씩 가져와 `[a,b]` 꼴로 쌍을 만들고 이 쌍을 나열한 배열을 반환한다.

### 예제
```js
R.xprod([1, 2], ['a', 'b']); //=> [[1, 'a'], [1, 'b'], [2, 'a'], [2, 'b']]
```
- `[1, 2]` `['a', 'b']`에서 원소를 하나씩 가져와 생성 가능한 모든 쌍 `[1, 'a']`, `[1, 'b']`, `[2, 'a']`, `[2, 'b']`을 만들어 배열에 담아 반환이 되었다.

## References
- https://ramdajs.com/docs/#xprod
