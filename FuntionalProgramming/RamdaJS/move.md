## move
> Move an item, at index from, to index to, in a list of elements. A new list will be created containing the new elements order.

## 설명

## 표현
```
Number → Number → [a] → [a]
```

## 예제
```js
R.move(0, 2, ['a', 'b', 'c', 'd', 'e', 'f']); //=> ['b', 'c', 'a', 'd', 'e', 'f']
R.move(-1, 0, ['a', 'b', 'c', 'd', 'e', 'f']); //=> ['f', 'a', 'b', 'c', 'd', 'e'] list rotation
```
- `0`번 인덱스를 2번 인덱스 자리로 옮긴다. 배열의 나머지 원소의 상대적 위치는 그대로이다. 하나의 원소가 이동이 되었기 때문에 이동된 원소를 제외한 나머지 원소의 인덱스도 자동으로 변경된다.

## Reference
- https://ramdajs.com/docs/#move
