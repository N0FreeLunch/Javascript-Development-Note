## length
> Returns the number of elements in the array by returning list.length.
- 배열 내의 원소의 갯수를 반환하며 내부적으로는 배열을 list라고 했을 때 list.length 값을 반환하는 동작을 한다.

## 설명
- 인자는 하나를 받으며 첫 번째 인자로 배열을 받아 함수를 평가하여 배열 내의 원소의 갯수를 반환한다.

## 표현
```
[a] → Number
```
- 첫 번째 인자로 임의의 원소가 들어 있는 배열을 받고 `[a] →`
- `→ Number` 배열 내의 원소의 갯수를 반환한다.

## 예제
```
R.length([]); //=> 0
R.length([1, 2, 3]); //=> 3
```
- `[]`는 원소가 없는 배열이므로 `0`을 반환한다.
- `[1, 2, 3]`은 원소가 3개 있는 배열이므로 `3`을 반환한다.

## Reference
- https://ramdajs.com/docs/#length
