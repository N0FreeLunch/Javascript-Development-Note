## remove
> Removes the sub-list of list starting at index start and containing count elements. Note that this is not destructive: it returns a copy of the list with the changes. No lists have been harmed in the application of this function.

> See also without.

> Open in REPLRun it here

### 설명

### 표현
```
Number → Number → [a] → [a]
```
- `Number →`: 첫 번째 인자로 제거하기 시작할 인덱스 번호를 받는다.
- `→ Number →`: 두 번째 인자로 첫 번째로 받은 인덱스 부터 뒤따르는 몇 개의 원소를 삭제할지를 지정한다.
- `→ [a] →`: 대상 배열을 지정한다.
- `→ [a]`: 세 번째 인자로 받은 배열에서 첫 번째 인자의 인덱스의 원소부터 시작하여 두 번째 인자로 받은 갯수만큼 원소를 삭제한 원소를 나열한 배열을 반환한다.

### 예제
```
R.remove(2, 3, [1,2,3,4,5,6,7,8]); //=> [1,2,6,7,8]
```
- 첫 번째 인자로 받은 2는 2번 인덱스를 의미한다. 배열에서 `3`에 해당한다.
- 두 번째 인자로 받은 3은 3개를 의미한다. 첫 번째 인자로 선택된 인덱스에 해당하는 값 3부터 4,5까지를 제거한다.
- `[1,2,3,4,5,6,7,8]`에서 `[1,2,(3,4,5),6,7,8]`인 괄호를 친 부분만을 제거하여 `[1,2,6,7,8]`이란 결과가 반환된다.

## Reference
- https://ramdajs.com/docs/#remove
