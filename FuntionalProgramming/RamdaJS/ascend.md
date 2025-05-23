## ascend

> Makes an ascending comparator function out of a function that returns a value that can be compared with < and >.
- 오름차순으로 정렬하기 위한 비교함수를 만든다. (비교기호) < 와 > 로 비교할 수 있는 값을 반환하는 함수가 비교 함수가 된다.

> See also [descend](./descend.md).

### 설명

- sort와 같은 정렬 함수의 나열 순서를 결정하기 위해 사용되는 비교 함수(comparator functio)를 만들기 위해 사용되는 함수이다. 비교함수는 두 값을 받아서 수를 반환하며, 정렬 함수는 반환된 수가 양수이면 받은 두 값의 순서를 교체하고 반환된 수가 음수이면 받은 두 값의 순서를 그대로 둔다. 이런 정렬함수의 비교함수로 오름차순의 나열을 하기 위해서 두 수를 받아 나중에 받은 값에서 먼저 받은 값을 뺀 결과값을 반환한다.
- ascend 함수는 오름차순을 만들기 위한 비교함수를 만들며, 함수를 하나 받아서 두 값을 받는 비교함수를 반환한다. 이 때 함수는 리스트의 요소를 전달 받았을 때 순서 비교가 가능한 값을 반환하는 함수이다.
- ascend 함수는 총 3개의 인자를 받지만, 첫 번째 인자만 받을 경우, 두 개의 인자를 받는 비교함수가 되므로 모든 인자를 받아 평가하는 방식으로 쓰이지 않고 비교함수를 만들어 정렬 함수에 전달하는 용도로 사용한다.

### 문법

```
R.ascend(fn, a, b): Number
```
- `fn`: A function of arity one that returns a value that can be compared
- `a`: The first item to be compared.
- `b`: The second item to be compared.
- Returns Number `-1` if fn(a) < fn(b), `1` if fn(b) < fn(a), otherwise `0`

### 표현

```
Ord b => (a → b) → a → a → Number
```
- `Ord b => ` 순서를 정할 수 있는 종류 b에 대해서
- `(a → b) →`: 첫 번째 인자로는 어떤 값(a)을 받아서 순서를 정할 수 있는 종류의 값(b)을 반환하는 함수를 받는다.
- `→ a →`: 두 번째 인자로는 첫 번째 인자로 받은 함수의 인자로 전달할 수 있는 값을 받는다.
- `→ a →`: 세 번째 인자도 마찬가지로 첫 번째 인자로 받은 함수의 인자로 전달할 수 있는 값을 받는다.
- `→ Number`: 비교에 사용된는 수를 반환한다.
- 두 번째 인자를 첫 번째 함수에 넣어 반환된 값과 세 번째 인자를 첫 번째 함수에 넣어 반환된 값을 서로 비교하며 오름차순이 되기 위해서는 두 번째 인자를 사용한 반환 값에서 세 번째 인자를 사용한 반환 값을 뺐을 때 양수를 반환하면 큰 순서대로 나열된다. 예를 들어 '5 - 3 = 양수'이다. 따라서 5는 3보다 크다.
- 일반적으로 비교 함수는 sort 함수에 전달해서 사용한다. sort 함수에 전달되는 비교함수가 오름차순으로 나열하기 위해서는 두 인자를 전달 받아서 첫 번째 인자에서 두 번째 인자를 뺀 값이 양수가 되면 첫 번째 인자 다음에 두 번째 인자를 나열하여 오름차순의 순서를 유지하고 첫 번째 인자에서 두 번째 인자를 뺀 값이 음수인 경우에는 두 번째 인자 다음에 첫 번째 인자를 나열해야 한다.
- ascend 함수가 인자로 함수를 하나 받으면 두 값을 받는 함수가 되는데 두 값을 인자로 받은 함수에 전달한 결과 값을 서로 비교하여 두 값중 먼저 받은 값에서 나중에 받은 값을 뺀 결과에 부호를 반대로 한 값을 반환한다. 예를 들어 - (5 - 3) 은 -2이다. 이 때 sort는 순서를 유지하므로 5, 3의 순서 그대로가 되고 - (4 - 7) = 3이다. 이 때 sort는 순서를 바꾸므로 7, 4의 순으로 나열되는 것이다.

### 예제

```js
const byAge = R.ascend(R.prop('age'));
const people = [
  { name: 'Emma', age: 70 },
  { name: 'Peter', age: 78 },
  { name: 'Mikhail', age: 62 },
];
const peopleByYoungestFirst = R.sort(byAge, people);
  //=> [{ name: 'Mikhail', age: 62 },{ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 }]
```
- `R.prop('age')`는 프로퍼티를 추출할 수 있는 대상을 받아 대상이 가진 `age`라는 프로퍼티의 값을 반환하는 함수이다.
- `R.ascend(R.prop('age'))`는 프로퍼티를 추출할 수 있는 인자 두 개를 받아 `R.prop('age')`에 각각 전달한 값을 서로 비교하여 큰 작은 값을 먼저 나열하도록 한다.
- `R.sort` 함수는 비교 함수를 받는데, `R.ascend`을 사용한 오름차순으로 정렬하기 위한 비교 함수를 받았으므로 오름차순으로 정렬한다. `R.sort(byAge, people)` 따라서 `age` 프로퍼티 값이 작은 대상부터 순서대로 `{ name: 'Mikhail', age: 62 }`, `{ name: 'Peter', age: 78 }`, `{ name: 'Emma', age: 70 }`의 순이 된다.

## References
- https://ramdajs.com/docs/#ascend
- https://github.com/ramda/ramda/blob/master/test/ascend.js
- https://github.com/ramda/types/blob/develop/types/ascend.d.ts
