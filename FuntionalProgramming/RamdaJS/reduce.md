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
- 세 번째 인수에 reduce 메서드가 있으면 해당 메서드로 디스패치합니다. 이 경우, reduce에서 R.reduced 단축을 구현하지 않으므로 사용자가 이를 처리해야 합니다.

> See also reduced, addIndex, reduceRight.

### 설명

### 표현
```
((a, b) → a) → a → [b] → a
```

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

## Reference
- https://ramdajs.com/docs/#reduce
