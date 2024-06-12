## reduceWhile
> Like reduce, reduceWhile returns a single item by iterating through the list, successively calling the iterator function. reduceWhile also takes a predicate that is evaluated before each step. If the predicate returns false, it "short-circuits" the iteration and returns the current value of the accumulator. reduceWhile may alternatively be short-circuited via reduced.
- reduce와 마찬가지로 reduceWhile도 리스트를 순회하면서 순회 함수가 잇달아서 호출이 되고, (최종적으로) 단일한 값(item)을 반환한다. reduceWhile은 술어 함수를 하나 받는데, 이 술어 함수는 각 단계를 평가한다. 만약 주어진 술어 함수가 false를 반환하면, 순회를 일찍 끝내며 (short-circuits), 누산기의 현재 값 (순회가 중단된 부분까지의 누산기 값)을 반환한다. reduceWhile은 reduced를 이용하여 (순회를) 일찍 끝내는 방식 대신에 사용될 수 있다.

> See also reduce, reduced.

### 설명
- reduce와 유사한 동작을 하지만 각 순회 단계를 진행하기 전에 계산을 더 수행할지 수행하지 않을지 결정할 수 있는 술어 함수를 먼저 동작시킨다. 술어함수가 참이면 해당 단계의 순회 함수를 실행하고 다음 단계의 순회를 계속진행하며, 술어함수가 거짓이면 해당 단계의 순회 함수를 실행하지 않고 다음 단계의 순회를 진행하지 않는다. 그리고 결과 값으로 멈춘 단계까지 계산된 마지막 누산기 값을 반환한다.
- 프로그래밍 문법의 while을 보자. `while (condition) { statement }` condition이 true인 경우에만 {} 내부의 statement를 실행하며, 조건이 false이면 반복을 멈추게 된다. {}의 코드의 실행이 완료되면 condition이 참이라면 {} 내부의 statement를 반복해서 실행한다. 마찬가지로 주어진 술어함수가 참을 만족할 때만 순회 함수를 실행하도록 하며, 술어함수가 거짓일 경우 순회 함수를 실행하지 않으며 순회를 종료한다. 이런 유사한 방식으로 인해 reduceWhile이란 이름이 부여되었다. 이 때 반환 값으로 누산기의 최종값을 반환하며, 술어함수에 전달된 누산기 값을 반환하며, 술어 함수가 거짓으로 판단 되었기 때문에 순회 함수가 동작하지 않아 해당 순회에서의 순회 함수의 계산된 반환 값이 아닌 이전 순회 단계의 순회함수의 반환 값을 최종 반환 값으로 반환하게 된다.

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
- `isOdd`는 주어진 값이 홀수인지 판별하는 순회함수이다. reduceWhile의 술어 함수로 사용되기 위해서 누산기 값을 첫 번째 인자로 받도록 인자를 추가한 형태가 되었다.
- 첫 번째 순회에서 누산기의 초기값은 0, 대상 원소는 1이다. 술어 함수에 전달 했을 때 `isOdd(0, 1)`으로 true가 된다. 따라서 순회 함수를 동작하며, `R.add(0, 1)`으로 1을 다음 순회의 누산기 값으로 전달한다.
- 두 번째 순회에서 이전 순회에서 전달된 누산기 값은 1이며, 대상 원소는 3이다. 술어 함수는 `isOdd(1, 3)`으로 true가 된다. 따라서 순회 함수를 동작하며, `R.add(1, 3)`으로 4를 다음 순회의 누산기 값으로 전달한다.
- 세 번째 순회에서 이전 순회에서 전달된 누산기 값은 4이며, 대상 원소는 5이다. 술어 함수는 `isOdd(4, 5)`으로 true가 된다. 따라서 순회 함수를 동작하며, `R.add(4, 5)`으로 9를 다음 순회 함수의 누산기 값으로 전달한다.
- 네 번째 순회에서 이전 순회에서 전달된 누산기 값은 9이며, 대상 원소는 60이다. 술어 함수는 `isOdd(9, 60)`으로 false가 된다. 따라서 순회 함수를 동작하지 않고 모든 순회를 멈추며, 술어 함수에 전달 받은 누산기 값을 반환하므로 9가 최종 반환값이 된다.

## Reference
- https://ramdajs.com/docs/#reduceWhile
