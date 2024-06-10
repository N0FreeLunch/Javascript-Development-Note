## reduceRight
> Returns a single item by iterating through the list, successively calling the iterator function and passing it an accumulator value and the current value from the array, and then passing the result to the next call.
- 리스트를 순회하며 단일한 값(item)을 반환한다. 순회 함수가 성공적으로 호출이 되면 순회 함수에는 누산기(accumulator) 값과 배열에서의 현재의 값 (리스트에서 처리할 대상 원소)을 전달한며, 순회 함수의 반환 값은 다음 순회 함수가 호출될 때 (누산기 값으로) 전달된다.

> Similar to reduce, except moves through the input list from the right to the left.
- reduce 함수와 비슷하지만, 주어진 입력 리스트를 오른쪽에서 왼쪽으로 처리한다.

> The iterator function receives two values: (value, acc), while the arguments' order of reduce's iterator function is (acc, value). reduceRight may use reduced to short circuit the iteration.
- 순회 함수는 (value, acc)라는 두 값을 받는 반면, reduce의 순회 함수의 인수 순서는 (acc, value)이다. reduceRight는 reduced 함수를 사용하여 간략(short circuit)한 순회의 사용할 수 있다.

> Note: R.reduceRight does not skip deleted or unassigned indices (sparse arrays), unlike the native Array.prototype.reduceRight method. For more details on this behavior, see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight#Description
- R.reduce는 네이티브 Array.prototype.reduce 메서드와 달리 삭제되거나 또는 할당되지 않은 인덱스들 (일부 원소가 비어 있는 배열)을 건너뛸 수 없다. 더 자세한 사항은 `https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#Description`을 보라


> Be cautious of mutating and returning the accumulator. If you reuse it across invocations, it will continue to accumulate onto the same value. The general recommendation is to always return a new value. If you can't do so for performance reasons, then be sure to reinitialize the accumulator on each invocation.

- 누산기(accumulator, 누적되는 값으로 생각하면 된다.)의 반환하거나 변경할 때는 주의할 점이 있다. 만약 누산기(accumulator)를 여러 번 (원소를 순회 하면서 순회 함수의 적용을) 반복하는 동안 재사용하는 경우 누산기(accumulator)는 계속해서 같은 값을 누적할 것이다. 일반적인 권장사항은 항상 새로운 값을 반환하도록 하는 것이다. 성능상의 이유로 (대상을 복사하거나 새로운 값을 생성하는 방식을 사용)할 수 없다면, 누산기가 호출 될 때 반드시 초기화를 해야 한다.

> See also reduce, addIndex, reduced.

### 설명

### 표현
```
((a, b) → b) → b → [a] → b
```

### 예제
```js
R.reduceRight(R.subtract, 0, [1, 2, 3, 4]) // => (1 - (2 - (3 - (4 - 0)))) = -2
//    -               -2
//   / \              / \
//  1   -            1   3
//     / \              / \
//    2   -     ==>    2  -1
//       / \              / \
//      3   -            3   4
//         / \              / \
//        4   0            4   0
```
- `R.subtract`는 첫 번째 인자 값에서 두 번째 인자 값을 뺀다. `R.subtract`는 순회 함수로 사용 되었다. 첫 번째 인자는 누산기 값으로 이전 순회함수의 결과 값이가 누산기의 초기값을 전달 받으며, 두 번째 인자는 현재 배열의 현재 순회 대상을 전달 받는다.
- 두 번째 인자로는 누산기의 초기값을 받았다. 세 번째로는 순회할 배열을 받는다.
- 일반적인 reduce의 경우 (((0 - 1) - 2) - 3) - 4의 순서로 계산이 된다. 하지만 reduceRight의 경우에는 순회를 배열의 마지막부터 시작하고 누산기의 초기값도 마지막 원소에 적용되는 순회 함수에 전달 된다. 또한 순회 함수의 인자를 반대로 받기 때문에 1 -(2 - (3 - (4 - 0)))의 순서로 계산된다.

## Reference
- https://ramdajs.com/docs/#reduceRight
