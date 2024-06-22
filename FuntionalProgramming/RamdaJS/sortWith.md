## sortWith
> Sorts a list according to a list of comparators.
- 정렬기(comparators)를 사용해서 리스트를 정렬한다.

> See also ascend, descend.

### 설명
- 데이터베이스 쿼리문의 'order by'가 나열된 컬럼을 먼저 나열된 컬럼을 정렬하고 순서의 선후를 구분할 수 없는 경우 다음 커럼을 기준으로 정렬을 하는 것과 같이, 나열된 정렬기의 순서에 따라 정렬하며 정령의 선후를 구분할 수 없는 경우 다음 정렬기를 사용해서 정렬한다.

### 표현
```
[(a, a) → Number] → [a] → [a]
```
- `[(a, a) → Number] →`: `(a, a) → Number`는 정렬기(comparator)에 해당한다. 정렬기의 두 번째 인자에서 첫 번째 인자를 뺀 값이 양수이면 두 번째 값이 첫 번째 값 보다 큰 것으로 순서를 그대로 유지하고, 음수이면 순서를 바꾸는 역할을 갖는다. 정렬기 원소로 한 배열을 받는데, 이는 첫 번째 정렬기에 의해 순서가 정해지지 않는 경우 두 번째 정렬기에 의해 순서를 정하는 것으로 서로 비교의 순위를 결정할 수 없을 때 다음 정렬기를 사용하여 순위를 정한다. 두 번째 배열의 원소를 인자로 받기 때문에 타입 파라메터로 `(a, a)`를 받는다.
- `→ [a] →`: 두 번째 인자로 정렬할 대상 배열을 받는다.
- `→ [a]`: 정렬된 배열이 반환된다.

### 예제
```js
const alice = {
  name: 'alice',
  age: 40
};
const bob = {
  name: 'bob',
  age: 30
};
const clara = {
  name: 'clara',
  age: 40
};
const people = [clara, bob, alice];
const ageNameSort = R.sortWith([
  R.descend(R.prop('age')),
  R.ascend(R.prop('name'))
]);
ageNameSort(people); //=> [alice, clara, bob]
```
- 위의 예제는 `R.descend(R.prop('age'))`으로 'age' 프로퍼티의 값을 기준으로 내림차순 정렬을 하며 이 기준으로 정렬되지 않는 경우 `R.ascend(R.prop('name'))`으로 'name' 프로퍼티를 기준으로 오름차순 정렬을 한다.
- 따라서 'age'가 40인 alice와 clara가 먼저 나열되며, 그 다음에 bob이 나열된다. 그런데 나이로는 alice와 clara가 동일하므로 순서가 결정되지 않는다. 따라서 다음 기준인 'name'에 따라서 정렬한다. 'name' 프로퍼티의 값인 'alice'가 'bob'을 비교하면 오브젝트의 순서는 alice, clara, bob의 순서가 된다.

## Reference
- https://ramdajs.com/docs/#sortWith
