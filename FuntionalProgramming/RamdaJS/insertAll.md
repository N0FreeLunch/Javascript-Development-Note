## insertAll
> Inserts the sub-list into the list, at the specified index. Note that this is not destructive: it returns a copy of the list with the changes. No lists have been harmed in the application of this function.

## 표현
```
Number → [a] → [a] → [a]
```

## 설명
- `insert`가 하나의 원소를 주어진 배열에 넣는 것과 달리 `insertAll`은 여러 원소를 배열로 받아 이를 주어진 배열의 원소로 넣는다.
- 첫 번째 인자는 두 번째 인자의 배열의 원소들을 넣을 첫 번째 위치를 지정한다.
- 두 번째 인자는 세 번째 인자로 받는 배열에 넣을 원소를 나열한 배열을 받는다.
- 세 번째 인자는 추가될 원소를 받는 배열을 지정한다.
- 세 번째 인자의 배열에 두 번째 인자의 배열 원소를 지정한 인덱스부터 차례로 나열한다. 기존의 인덱스 번호에서 넣어진 원소로 인해 넣어진 원소의 수 만큼 인덱스 번호가 뒤로 밀린다.

## 예제
```
R.insertAll(2, ['x','y','z'], [1,2,3,4]); //=> [1,2,'x','y','z',3,4]
```
- `[1, 2, 3, 4]`의 2번 인덱스 부터 `['x','y','z']`의 원소를 차례로 나열해서 `1,2,'x','y','z'`가 되며 `3,4`는 `'x','y','z'`가 들어온 만큼 뒤로 밀리게 된다. 따라서 `[1,2,'x','y','z',3,4]`이다.

## Reference
- https://ramdajs.com/docs/#insertAll
