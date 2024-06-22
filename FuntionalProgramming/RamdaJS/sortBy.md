## sortBy
> Sorts the list according to the supplied function.
- 주어진 함수에 따라 리스트를 정렬한다.

### 설명
- 리스트를 받아 배열 안의 원소를 원소를 넣으면 그 반환 값으로 순서를 가진 대상을 반환 하는 함수에 넣어 반환된 순서대로 원소가 나열된 리스트를 반환한다.

### 표현
```
Ord b => (a → b) → [a] → [a]
```
- `Ord b =>`: 순서가 정해진 타입 파라메터 b에 대해
- `(a → b) → `: 첫 번째 인자로 정렬을 위한 함수를 받는다. 이 함수는 배열의 원소를 받아서 반환된 값의 순서대로 정렬을 헤야 하므로 배열의 원소와 같은 타입 파라메터인 a를 인자로 받고 정렬 가능한 타입 파라메터인 b를 반환한다.
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

#### 첫 번째 예제
- `R.prop(0)` 함수의 반환 값은 인자를 하나 받아 0번 인덱스를 추출하는 함수이다. `R.sortBy(R.prop(0))`는 첫 번째 인자의 크기 순으로 비교하게 된다. `sortByFirstItem`으로 이름이 붙여졌는데, 0번 인덱스의 대상 곧 첫 번째 값을 기준으로 정렬하는 함수로 명명된 것을 알 수 있다.
- `[[-1, 1], [-2, 2], [-3, 3]]`에서 각 원소의 첫 번쨰 아이템은 `-1`, `-2`, `-3`이 된다. 작은 순으로 나열하면 `-3`, `-2`, `-1`이 된다. 이 순대로 대응되는 아이템을 나열하면 `[[-3, 3], [-2, 2], [-1, 1]]`가 된다.

#### 두 번째 예제
- `R.sortBy(R.compose(R.toLower, R.prop('name')))`를 해석하면, `R.compose`는 오른쪽에 나열된 함수를 평가하여 그 결과를 왼쪽의 함수로 넘겨 주는 역할을 한다. 따라서 `R.compose(R.toLower, R.prop('name'))`는 대상에서 name이란 프로퍼티의 값을 뽑아 그 결과를 `R.toLower`에 전달하므로 소문자로 바꾼다. 이런 대상을 `R.sortBy` 하므로 name 프로퍼티에 대응하는 값을 대문소문자와 대문자의 조합으로 정렬하지 않고, 소문자의 순서만을 고려한 정렬을 한다. 프로그래밍에서 'CaseInsensitive'란 단어는 대소문자를 구분하지 않음을 뜻한다. `sortByNameCaseInsensitive`로 함수가 명명된 이유는 문자열에 포함된 모든 문자를 소문자로 바꾸어 정렬하기 때문에 대소문자에 의한 순서의 변경 없이, 소문자로만 순서를 판단하므로 영어 알파벳의 순서를 따른다. 따라서 대 소문자의 순서 구분 없이 그냥 영어의 의미상 순서를 따르게 되는 것이다.
- `sortByNameCaseInsensitive`으로 `[clara, bob, alice]`을 정렬하면, 각 오브젝의 `name` 프로퍼티는 `'ALICE'`, `'Bob'`, `'clara'`이므로  'alice', 'bob', 'clara'으로 정렬된다. 이 순에 따라서 이 값을 갖고 있는 각각의 오브젝트도 해당 순으로 나열되어 `[alice, bob, clara]`가 된다.

## Reference
- https://ramdajs.com/docs/#sortBy
