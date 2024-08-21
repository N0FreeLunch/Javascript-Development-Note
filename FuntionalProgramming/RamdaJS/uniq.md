## uniq
> Returns a new list containing only one copy of each element in the original list.
- 원본 리스트에 있는 원소 각각에 대해 하나의 복사본만을 가지는 새로운 리스트를 반환한다. 

> R.equals is used to determine equality.
- 동등성을 결정할 때는 R.equals가 사용된다.

### 설명

### 표현

### 예제
```js
R.uniq([1, 1, 2, 1]); //=> [1, 2]
R.uniq([1, '1']);     //=> [1, '1']
R.uniq([[42], [42]]); //=> [[42]]
```
- `[1, 1, 2, 1]`에서 서로 `R.equals`에 의해 서로 동일하게 판별되는 대상은 0번, 1번, 3번 인덱스이다. 따라서 반환되는 각각의 원소는 하나의 복사본만을 가져야 하므로 `[1, 2]`가 반환된다.

## References
- https://ramdajs.com/docs/#uniq
