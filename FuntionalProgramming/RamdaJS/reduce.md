## reduce
> Returns a single item by iterating through the list, successively calling the iterator function and passing it an accumulator value and the current value from the array, and then passing the result to the next call.
- 리스트를 순회아혀 단일한 요소를 반환한다. 순회 함수(iterator function)를 연속적으로 호출하고 (이전 함수에서 전달된) 축적된 값과 배열에서의 현재값(리스트에서 처리 대상 원소)을 전달한다. 그리고 다음 (순회 함수를) 호출할 때 (이전 순회 함수의) 결과값을 전달한다.

> The iterator function receives two values: (acc, value). It may use R.reduced to shortcut the iteration.
- 순회 함수는 두 값(acc, value)을 받는다. 순회를 간략히하기 위해 R.reduced를 사용할 수 있다.

> The arguments' order of reduceRight's iterator function is (value, acc).
- reduceRight 순회 함수의 인자들의 순서는 (value, acc)이다.

> Note: R.reduce does not skip deleted or unassigned indices (sparse arrays), unlike the native Array.prototype.reduce method. For more details on this behavior, see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#Description
- R.reduce는 네이티브 Array.prototype.reduce 메서드와 달리 삭제되거나 또는 할당되지 않은 인덱스들 (일부 원소가 비어 있는 배열)을 건너뛸 수 없다. 더 자세한 사항은 `https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#Description`을 보라

> Be cautious of mutating and returning the accumulator. If you reuse it across invocations, it will continue to accumulate onto the same value. The general recommendation is to always return a new value. If you can't do so for performance reasons, then be sure to reinitialize the accumulator on each invocation.
- 누산기(accumulator)의 반환하거나 변경하는 것에 주의 해야 한다. 만약 누산기(accumulator)를 여러번 반복 되는 동안 재사용하는 경우 누산기(accumulator)는 계속해서 같은 값을 누적할 것이다. 일반적인 권장사항은 항상 새로운 값을 반환하도록 하는 것이다. 성능상의 이유로 그렇게 할 수 없다면, 누산기가 호출 될 때 반드시 초기화를 해야 한다.

> Dispatches to the reduce method of the third argument, if present. When doing so, it is up to the user to handle the R.reduced shortcuting, as this is not implemented by reduce.
- 만약 reduce 메소드의 세번째 인자가 존재하면 reduce 메소드의 세번째 발동한다. 만약 발동(디스패치)된다면 reduce로 구현되지 않으므로 유저는 R.reduced를 사용한 단축을 다룰 수 없다. 

> See also reduced, addIndex, reduceRight.

### 설명
- 배열에 나열된 원소의 순서대로 순회 함수를 적용하며, 순회 함수의 실행 결과값을 그 다음 원소에 대한 순회함수에 전달하면서, 다음 요소에 대한 순회 함수는 이전 요소에 대한 순회 함수가 만든 결과 값을 전달하는 방식으로 값을 누산하여 최종적인 결과값을 만드는 함수이다.

### 표현
```
((a, b) → a) → a → [b] → a
```
- `((a, b) → a)`: 첫 번째 인자로 순회 함수를 받는다. 순회 함수는 이전 순회 함수의 연산의 결과로 전달된 누적된 값을 인자로 받는 `a`와 순회 하면서 처리할 대상 요소 `b`를 받아 그 다음 차혜의 순회에서 순회 함수가 처리될 때 첫 번째 인자 `a`로 전달할 수 있는 종류의 값` a`을 반환해야 한다.
- `→ a →`: 두 번째 인자로 누산을 적용할 초기값을 받는다. 순회 함수가 처음 실행될 때 이전 순회 함수의 결과값이 존재하지 않으므로 순회 함수는 이 초기값을 인자로 전달 받는다.
- `→ [b] →`: 세 번째 인자로 순회할 대상 배열을 전달받는다. 배열의 각 요소는 순회 함수의 두 번째 인자로 전달되므로 순회 함수의 두 번째 파라메터와 동일한 종류인 `b`가 된다.
- `→ a`: 세 번째 인자로 받은 배열의 요소가 모두 순회 함수를 거친 후 마지막 요소에 대한 순회 함수가 실행된 결과값을 반환한다.

### 예제
```js
R.reduce(R.subtract, 0, [1, 2, 3, 4]) // => ((((0 - 1) - 2) - 3) - 4) = -10
//          -               -10
//         / \              / \
//        -   4           -6   4
//       / \              / \
//      -   3   ==>     -3   3
//     / \              / \
//    -   2           -1   2
//   / \              / \
//  0   1            0   1
```
- `R.subtract`는 첫 번째 인자에서 두 번째 인자를 빼는 연산을 하는 함수이다. `R.reduce`의 첫 번째 인자로 할당되었으므로 누산된 값에서 순회의 현재 요소의 값을 빼는 연산을 한다.
- 두 번째 인자의 `0`은 누산의 초기값이며, 순회 대상은 `[1, 2, 3, 4]`으로 주어졌다.
- `[1, 2, 3, 4]` 첫 번째 순회는 요소 1에 대한 연산이다. 초기 순회 함수에는 이전 순회 함수의 결과값이 존재하지 않기 때문에 초기값 0을 이용하고 0에서 첫 번째 요소 1을 빼는 연산을 하므로 `0 - 1`이 된다.
- 두 번째 순회는 요소 2에 대한 연산이다. 이전 순회함수의 결과 값 `(0 - 1)`에서 2를 빼므로 `(0 - 1) - 2`가 된다.

## Reference
- https://ramdajs.com/docs/#reduce
