## sortBy
> Sorts the list according to the supplied function.
- 주어진 함수에 따라 리스트를 정렬한다.

### 설명

### 표현
```
Ord b => (a → b) → [a] → [a]
```
- `Ord b =>`: 순서가 정해진 타입 파라메터 b에 대해
- `(a → b) → `: 첫 번째 인자로 정렬을 위한 함수를 받는다.
- `→ [a] →`: 두 번째 인자로 정렬할 리스트를 받는다.
- `→ [a]`: 정렬된 리스트를 반환한다.

### 예제
```js
const sortByFirstItem = R.sortBy(R.prop(0));
const pairs = [[-1, 1], [-2, 2], [-3, 3]];
sortByFirstItem(pairs); //=> [[-3, 3], [-2, 2], [-1, 1]]

const sortByNameCaseInsensitive = R.sortBy(R.compose(R.toLower, R.prop('name')));
const alice = {
  name: 'ALICE',
  age: 101
};
const bob = {
  name: 'Bob',
  age: -10
};
const clara = {
  name: 'clara',
  age: 314.159
};
const people = [clara, bob, alice];
sortByNameCaseInsensitive(people); //=> [alice, bob, clara]
```
- `R.prop(0)` 함수의 반환 값은 인자를 하나 받아 0번 인덱스를 추출하는 함수이다. `R.sortBy(R.prop(0))`는 첫 번째 인자의 크기 순으로 비교하게 된다. `sortByFirstItem`으로 이름이 붙여졌는데, 0번 인덱스의 대상 곧 첫 번째 값을 기준으로 정렬하는 함수로 명명된 것을 알 수 있다.
- `[[-1, 1], [-2, 2], [-3, 3]]`에서 각 원소의 첫 번쨰 아이템은 `-1`, `-2`, `-3`이 된다. 작은 순으로 나열하면 `-3`, `-2`, `-1`이 된다. 이 순대로 대응되는 아이템을 나열하면 `[[-3, 3], [-2, 2], [-1, 1]]`가 되는 것.

## Reference
- https://ramdajs.com/docs/#sortBy
