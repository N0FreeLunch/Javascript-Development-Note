## reduceRight
> Returns a single item by iterating through the list, successively calling the iterator function and passing it an accumulator value and the current value from the array, and then passing the result to the next call.
- 리스트를 순회하며 단일한 값(item)을 반환한다. 순회 함수가 성공적으로 호출이 되면 순회 함수에는 누산기(accumulator) 값과 배열에서의 현재의 값 (리스트에서 처리할 대상 원소)을 전달한며, 순회 함수의 반환 값은 다음 순회 함수가 호출될 때 (누산기 값으로) 전달된다.

> Similar to reduce, except moves through the input list from the right to the left.
- reduce 함수와 비슷하지만, 주어진 입력 리스트를 오른쪽에서 왼쪽으로 처리한다.

> The iterator function receives two values: (value, acc), while the arguments' order of reduce's iterator function is (acc, value). reduceRight may use reduced to short circuit the iteration.
- (reduceRight의) 순회 함수는 (value, acc)라는 두 값(인자)을 받는 반면, reduce의 순회 함수의 (인자) 순서는 (acc, value)이다. reduceRight는 reduced 함수를 사용하여 간략(short circuit)한 순회의 사용할 수 있다.

> Note: R.reduceRight does not skip deleted or unassigned indices (sparse arrays), unlike the native Array.prototype.reduceRight method. For more details on this behavior, see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight#Description
- R.reduce는 네이티브 Array.prototype.reduce 메서드와 달리 삭제되거나 또는 할당되지 않은 인덱스들 (일부 원소가 비어 있는 배열)을 건너뛸 수 없다. 더 자세한 사항은 `https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#Description`을 보라

> Be cautious of mutating and returning the accumulator. If you reuse it across invocations, it will continue to accumulate onto the same value. The general recommendation is to always return a new value. If you can't do so for performance reasons, then be sure to reinitialize the accumulator on each invocation.

- 누산기(accumulator, 누적되는 값으로 생각하면 된다.)의 반환하거나 변경할 때는 주의할 점이 있다. 만약 누산기(accumulator)를 여러 번 (원소를 순회 하면서 순회 함수의 적용을) 반복하는 동안 재사용하는 경우 누산기(accumulator)는 계속해서 같은 값을 누적할 것이다. 일반적인 권장사항은 항상 새로운 값을 반환하도록 하는 것이다. 성능상의 이유로 (대상을 복사하거나 새로운 값을 생성하는 방식을 사용)할 수 없다면, 누산기가 호출 될 때 반드시 초기화를 해야 한다.

> See also reduce, addIndex, reduced.

### 설명
- reduce 함수가 주어진 배열을 낮은 인덱스 부터 높은 인덱스 쪽으로 순회하는 것과 달리, reduceRight 함수는 주어진 배열을 높은 인덱스 부터 낮은 인덱스 쪽으로 순회 한다.
- reduce는 순차적으로 적용이 된다. 순회 함수의 계산 결과를 다음 순회 함수의 누산기로 전달하는 방식이기 때문에 이전 순회의 연산은 다음 순회 연산 보다 우선 적용된다. 수학에서 괄호는 연산의 우선순위를 결정하는데 사용되는데 `R.reduce(R.add, 0 [1, 2, 3])`라는 코드가 있다면 0+1 이 먼저 연산이 되고 (0+1)+2가 그 다음 연산이 되고, ((0+1)+2)+3이 그 다음에 연산이 된다. 배열의 앞에서 뒤로 가면서 연산의 우선 순위가 감소하는 특성을 갖는다. 그에 반해 reduceRight는 배열의 뒤에서 앞으로 가면서 연산의 우선 순위가 감소하는 특성을 갖는다. 이는 달리 말하면 배열의 앞에서 뒤로 가는 연산을 생각했을 때는 연산 우선 순위가 증가하는 특성을 갖는다고 설명할 수 있다. `R.reduceRight(R.add, 0 [1, 2, 3])`를 생각해 보면 1+(2+(3+0)) reduce와 reduceRight 둘 모두 배열의 앞에서 뒤로 식을 나열할 때 연산의 우선 순위를 앞 쪽이 가지게 할 것인지 뒤 쪽이 가지게 할 것인지의 차이를 갖는다.
- reduce 순회 함수가 누산기와 현재 요소를 인자로 전달 받는 반면, reduceRight의 순회 함수는 인자의 순서를 반대로 받는다. 현재 요소를 첫 번째 인자로 누산기를 두 번째 인자로 받는다. reduceRight와 reduce가 전체 연산식의 나열은 순서는 그대로 두면서 연산의 우선 순위만 달리 갖도록 만든다. 예를 들어 reduceRight의 순회 함수가 인자의 순서를 바꾸지 않는다고 해 보자. 그럼 `R.reduceRight(R.add, 0 [1, 2, 3])`눈 (0+3)+2+1의 식을 만들어 낸다. 하지만 이는 reduce가 만드는 식인 ((0+1)+2)+3와 항의 배치가 다르다. 덧셈이라 결과의 차이가 없어 보일 수 있지만 항의 나열은 그대로 두면서 연산의 우선순위만 다르게 만들 수 없는 것이다. reduce가 갖는 감소의 의미는 연산의 우선순위를 통해서 우선순위가 높은 연산은 결과값을 만들어 식을 구성하는 항을 줄여나간다는 의미이다. 식을 나열했을 때 항을 오른쪽에서 줄여 나갈 것인지 왼쪽으로 줄여나갈 것인지를 의미하기 때문에 reduceRight는 reduce와 동등한 항의 나열을 가져야 하므로 reduceRight의 순회 함수는 인자의 순서가 reduce와 반대가 되어야 항의 나열 순을 그대로 만들 수 있기 때문에 순회 함수가 전달 받는 인자의 순서가 달라진다.
- 이런 특성에서 볼 때, 누산기의 초기값은 reduce를 사용했을 때나, reduceRight를 사용했을 때나 연산의 우선순위 이외에는 서로 영향을 주지 않는 값을 사용하는 쪽이 reduce의 원론적인 의미를 더 잘 살린다고 볼 수 있다. 물론 누산기의 초기값은 필요에 따라 할당을 해도 상관은 없다.

### 표현
```
((a, b) → b) → b → [a] → b
```
- `((a, b) → b) →`: 첫 번째 인자로는 순회 함수를 받는다. reduce 함수의 순회 함수와 달리 reduceRight의 순회 함수는 인자를 반대로 받는데 a가 현재 순회 대상 원소를 전달 받고, b가 이전 순회 함수의 반환 값 또는 누산기의 초기값을 받는다.
- `→ b →`: 두 번째 인자로는 누산기의 초기값을 받는다. 첫 번째 순회 함수에 배열의 마지막 원소와 함께 이전 순회 함수의 반환 값이 없으므로 대신 초기값으로 사용되는 값이다.
- `→ [a] →`: 세 번째 인자로는 순회할 대상 배열을 받는다.
- `→ b`: 최종적으로는 누산기의 최종값을 반환한다. 누산기와 동일한 종류의 값 b를 반환한다. 누산기는 순회 함수의 결과값이자 순회 함수의 인자이다. 따라서 순회 함수를 거듭하더라도 누산기는 계산이 되고 축적이 되어야 한다. 이러한 종류를 하나의 종류로 보고 b라는 기호로 공통화 할 수 있다.

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
- 일반적인 reduce의 경우 (((0 - 1) - 2) - 3) - 4의 순서로 계산이 된다. 하지만 reduceRight의 경우에는 순회를 배열의 마지막부터 시작하고 누산기의 초기값도 마지막 원소에 적용되는 순회 함수에 전달 된다. 또한 순회 함수의 인자를 반대로 받기 때문에 1 - (2 - (3 - (4 - 0)))의 순서로 계산된다.
- 첫 번째 순회의 순회 함수는 순회 대상 원소인 4를 첫 번째 인자로 누산기의 초기값 0을 두 번째 인자로 받는다. (reduceRight는 reduce와 달리 인자의 순서를 반대로 받는다.) ｀R.subtract｀ 함수는 첫 번째 인자에서 두 번째 인자를 빼기 때문에 4 - 0이 된다.
- 두 번째 순회의 순회 함수는 순회 대상 원소인 3을 첫 번째 인자로 첫 번째 순회의 순회 함수의 반환 값인 4 - 0을 두 번째 인자로 받는다. 따라서 3 - (4 - 0)이 된다.
- 세 번째 순회의 순회 함수는 순회 대상 원소인 2를 첫 번째 인자로 두 번째 순회의 순회 함수의 반환 값인 3 - (4 - 0)을 두 번째 인자로 받는다. 따라서 2 - (3 - (4 - 0))이 된다.
- 네 번째 순횐의 순회 함수는 순회 대상원소인 1을 첫 번째 인자로 두 번째 순회의 순회 함수의 반환값인 2 - (3 - (4 - 0))를 두 번째 인자로 받는다. 따라서 1 - (2 - (3 - (4 - 0)))가 된다.
- 최종적으로 반환되는 결과는 누산기에 1 - (2 - (3 - (4 - 0)))가 적용된 -2를 반환한다.

## Reference
- https://ramdajs.com/docs/#reduceRight
