## lastIndexOf
- Returns the position of the last occurrence of an item in an array, or -1 if the item is not included in the array. R.equals is used to determine equality.

## 설명
- 주어진 배열의 뒤에서 부터 지정한 값을 찾은 값이 배열에서 몇 번째 인덱스에 위치하는지 반환한다.
- 만약 배열에서 지정한 값을 찾지 못한다면 `-1`을 반환한다.

## 표현
```
a → [a] → Number
```
- `a →` 첫 번째 인자로는 배열에서 찾을 값을 받는다.
- `→ [a] →` 두 번째 인자로는 배열을 받는다.
- `→ Number` 두 번째 인자로 받은 배열에서 첫 번째 인자의 값에 해당하는 값을 배열의 뒤에서 부터 찾아서 찾으면 해당 원소의 배열에서의 인덱스 번호를 반환한다.

## 예시
```
R.lastIndexOf(3, [-1,3,3,0,1,2,3,4]); //=> 6
R.lastIndexOf(10, [1,2,3,4]); //=> -1
```

## Reference
- https://ramdajs.com/docs/#lastIndexOf
