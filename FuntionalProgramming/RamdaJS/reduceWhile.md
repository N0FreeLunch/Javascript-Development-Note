## reduceWhile
> Like reduce, reduceWhile returns a single item by iterating through the list, successively calling the iterator function. reduceWhile also takes a predicate that is evaluated before each step. If the predicate returns false, it "short-circuits" the iteration and returns the current value of the accumulator. reduceWhile may alternatively be short-circuited via reduced.
- reduce와 마찬가지로 reduceWhile도 리스트를 순회하면서 순회 함수가 잇달아서 호출이 되고, (최종적으로) 단일한 값(item)을 반환한다. reduceWhile은 술어 함수를 하나 받는데, 이 술어 함수는 각 단계를 평가한다. 만약 주어진 술어 함수가 false를 반환하면, 순회를 일찍 끝내며 (short-circuits), 누산기의 현재 값 (순회가 중단된 부분까지의 누산기 값)을 반환한다. reduceWhile은 reduced를 이용하여 (순회를) 일찍 끝내는 방식 대신에 사용될 수 있다.

> See also reduce, reduced.

### 설명

### 표현
```
((a, b) → Boolean) → ((a, b) → a) → a → [b] → a
```
- `((a, b) → Boolean) →`: 첫 번째 인자로 술어 함수를 받는다. 이 술어 함수는 첫 번째 인자로 누산기를 전달 받고, 두 번째 인자로 순회 대상 값을 전달 받는다.
- `→ ((a, b) → a) →`: 두 번째 인자로 순회 함수를 받는다. 이 순회 함수는 첫 번째 인자로 누산기 값을, 두 번째 배열의 순회 대상 원소를 전달 받는다.
- `→ a → `: 세 번째 인자로 누산기의 초기값을 받는다. 
- `→ [b] → `: 네 번째 인자로 순회할 배열을 받는다. 순회할 배열의 원소를 b로 표현했는데 이 값이 순회 함수의 두 번째 인자로 전달되는 값이기 때문에 순회 함수의 두 번째 인자를 표현한 b와 동일한 종류이다.
- `→ a`: 최종 반환 값은 누산기의 최종값이며, 술어함수에 의해 순회가 중단된 부분까지의 순회 함수의 반환 값을 반환한다.

### 예제
```js
const isOdd = (acc, x) => x % 2 !== 0;
const xs = [1, 3, 5, 60, 777, 800];
R.reduceWhile(isOdd, R.add, 0, xs); //=> 9

const ys = [2, 4, 6]
R.reduceWhile(isOdd, R.add, 111, ys); //=> 111
```
- `isOdd`는 두 인자를 받아서 짝수인지 판별하는 술어 함수이다.

## Reference
- https://ramdajs.com/docs/#reduceWhile
