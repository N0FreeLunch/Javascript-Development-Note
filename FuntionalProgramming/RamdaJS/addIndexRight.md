# addIndexRight

> As with addIndex, addIndexRight creates a new list iteration function from an existing one by adding two new parameters to its callback function: the current index, and the entire list.
- addIndex와 같이, addIndexRight는 새로운 리스트 순회 함수를 생성한다. 이 콜백 함수에는 하나의 파라메터가 존재하는 상태이며, 두 개의 새로운 파라메터로 현재 인덱스 그리고 전체 리스트 추가한다.

> Unlike addIndex, addIndexRight iterates from the right to the left.
- addIndex와 달리 addIndexRight는 오른쪽에서 왼쪽으로 순회한다.

## 설명

- addIndex와 동일하지만, 배열의 왼쪽에서 오른쪽으로 순회하지않고, 오른쪽에서 왼쪽으로 순회하는 함수
- 리스트 순회 함수가 리스트의 원소만을 인자로 전달하는 경우, addIndex으로 해당 함수를 씌우면, 리스트 원소 뿐만 아나라, 인덱스 및 전체 리스트도 순회 함수의 인자로 전달한다.

## 문법

```
R.addIndexRight(fn): function
```

> `fn` : A list iteration function that does not pass index or list to its callback
- `fn` : 리스트 순회 함수로, 인덱스와 전체 (리스트)를 콜벡 함수로 전달하지 않는 함수이다.
> Returns function An altered list iteration function that passes (item, index, list) to its callback
- `function`을 반환핟다. 콜백함수로 `(item, index, list)`를 전달하는 리스트 순회함수로 바꾼다.

## 표현

```
((a … → b) … → [a] → *) → (a …, Int, [a] → b) … → [a] → *)
```
- `((a … → b) … → [a] → *)`:
- `(a …, Int, [a] → b) … → [a] → *)`: 

## 예시

```js
const revmap = (fn, ary) => R.map(fn, R.reverse(ary));
const revmapIndexed = R.addIndexRight(revmap);
revmapIndexed((val, idx) => idx + '-' + val, ['f', 'o', 'o', 'b', 'a', 'r']);
//=> [ '5-r', '4-a', '3-b', '2-o', '1-o', '0-f' ]
```

## References

- https://ramdajs.com/docs/#addIndexRight
- https://github.com/ramda/ramda/blob/master/test/addIndexRight.js
- https://github.com/ramda/types/blob/develop/types/addIndexRight.d.ts
