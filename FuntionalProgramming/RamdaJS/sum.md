## sum
> Adds together all the elements of a list.
- 리스트의 모든 원소들을 모두 더한다.
> See also reduce.

### 설명
- 수를 원소로 하는 배열을 받아 배열 안의 모든 원소드릐 합을 반환한다.

### 표현
```
[Number] → Number
```
- `[Number] →`: 첫 번째 인자로는 수를 원소로 하는 배열을 받는다.
- `→ Number`: 첫 번째 인자로 받은 모든 원소의 합을 반환한다.

### 예제
```js
R.sum([2,4,6,8,100,1]); //=> 121
```
- 2 + 4 + 6 + 8 + 100 + 1 = 121

## Reference
- https://ramdajs.com/docs/#sum
