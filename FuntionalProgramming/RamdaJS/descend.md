## descend
> Makes a descending comparator function out of a function that returns a value that can be compared with `<` and `>`.
- 내림차순 비교함수(comparator function)를 만든다. `<` and `>` 으로 비교할 수 있는 값을 반환하는 함수가 비교함수가 된다.

> See also [ascend](./ascend.md), [descendNatural](./descendNatural.md), [ascendNatural](./ascendNatural.md).

### 설명
- 주어진 값 리스트를 내림차순으로 나열하는 함수를 만든다.
- 첫 번째 인자로 함수를 받는다.
- 두 번째 인자와 세 번째 인자로는 첫 번째 인자의 함수의 인자로 넣을 값을 받는다.
- 첫번째 함수는 f, 두 번째 인자를 a, 세 번째 인자를 b라고 하면, f(a) 값과 f(b)의 값을 서로 비교한다.
- 각각의 함수를 평가한 값이 f(a) > f(b) 이면 1을 반환하면 순서가 그대로
- 각각의 함수를 평가한 값이 f(a) = f(b) 이면 0을 반환하면 순서가 그대로
- 각각의 함수를 평가한 값이 f(a) < f(b) 이면 -1을 반환하면 순서를 바꾼다.

### 문법
```
R.descend(fn, a, b): Number
```
- fn: A function of arity one that returns a value that can be compared
- a: The first item to be compared.
- b: The second item to be compared.
- Returns Number `-1` if fn(a) > fn(b), `1` if fn(b) > fn(a), otherwise `0`

### 표현
```
Ord b => (a → b) → a → a → Number
```
- `Ord b =>` 타입 `b`는 순서가 있는 집합의 원소이다. 서로 크기를 비교할 수 있다.
- `(a → b) →` 첫 번째 인자로 함수를 받는다.
-  `→ a →` 두 번째 인자로 첫 번째 인자의 함수의 인자로 들어가는 타입과 같은 타입 `a`값을 받는다.
-  `→ a →` 세 번째 인자로 첫 번째 인자의 함수의 인자로 들어가는 타입과 같은 타입 `a`값을 받는다.
-  `(a → b)` 함수에 인자로 두 번째 인자로 타입 `a`를 넣어 평가한 결과와 세 번째 인자로 타입 `a`를 넣어 평가한 결과를 비교하여 비교 결과에 따라 수를 반환한다.

### 예제
```js
const byAge = R.descend(R.prop('age'));
const people = [
  { name: 'Emma', age: 70 },
  { name: 'Peter', age: 78 },
  { name: 'Mikhail', age: 62 },
];
const peopleByOldestFirst = R.sort(byAge, people);
  //=> [{ name: 'Peter', age: 78 }, { name: 'Emma', age: 70 }, { name: 'Mikhail', age: 62 }]
```
- `R.prop('age')`는 첫번째 인자로 오브젝트에서 뽑을 키를 지정하고 두 번째 인자로는 대상 오브젝트를 지정하여 선택한 키의 값을 뽑는 함수이다.
- `R.descend`는 첫 번째 인자로 함수를 지정한다. 이 함수는 인자를 하나 받아 평가되는 함수이다. 두 번째 인자와 세 번째 인자는 첫 번째 인자의 함수에 들어갈 인자를 받는다. 
- `R.descend`는 내부적으로 첫 번째 인자의 함수의 인자로 두 번째 인자를 받은 것과 세 번째 인자의 함수의 인자로 받은 값을 각각 넣고 평가한 값의 크기를 비교한다. 두 번째 인자를 넣은 함수의 값이 세 번째 인자를 넣은 값보다 크면 1 아니면 -1을 반환하며 평가된 두 값이 같으면 0을 반환한다.
- `byAge`는 두 개의 오브젝트 인자를 받아 오브젝트에서 `age`키의 값을 취득한 다음 서로 비교하여 `-1`, `0`, `1`을 반환하는 함수이다.
- `R.sort` 비교를 위한 함수와 비교할 대상의 리스트를 받는다. 비교 대상의 리스트의 두 개씩 차례로 뽑는데 첫 번째와 두 번째, 첫 번째와 두 번째를 비교한 값 중 작은 값을 두 번째로 두고 세번째와 비교하여 더 작은 값을 세 번째로 두고 네번째와 비교하는 방식을 사용한다. 대상이 되는 두 개의 원소는 비교를 위한 함수에 넣는데 함수의 평가 값이 0보다 크거나 같으면 `R.sort` 함수는 순서를 그대로 두고 0보다 작으면 순서를 바꾸는 연산을 한다.

#### 상세
- `R.sort`함수는 내부적으로 `byAge` 함수의 첫 번째 인자로 `{ name: 'Emma', age: 70 }`를, 두 번째 인자로 `{ name: 'Peter', age: 78 }`를 할당한다.
- `byAge` 함수는 받은 오브젝트 인자에서 `age` 키애 해당하는 값을 뽑아 서로 비교한다. `byAge`함수는 내부적으로 `R.prop('age')`에 의해 `70`과 `78`을 뽑고 `R.descend`함수를 사용하기 때문에 `-1`을 반환한다.
- `R.sort`함수는 내부적으로 `{ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 }`의 순서를 바꾸어 `{ name: 'Peter', age: 78 }, { name: 'Emma', age: 70 }`의 순이 되게 한다.
- 다음으로 `byAge` 함수에 `{ name: 'Emma', age: 70 }`을 첫 번째 인자로 `{ name: 'Mikhail', age: 62 }`를 두 번째 인자로 할당한다. `R.prop('age')`에 의해 `70`과 `62`가 뽑히고 `R.descend`에 의해 1을 반환하므로 순서를 바꾸지 않는다.
- 따라서 최종 결과는 `[{ name: 'Peter', age: 78 }, { name: 'Emma', age: 70 }, { name: 'Mikhail', age: 62 }]`이 되는 것.

## References
- https://ramdajs.com/docs/#descend
- https://github.com/ramda/ramda/blob/master/test/descend.js
- https://github.com/ramda/types/blob/develop/types/descend.d.ts
