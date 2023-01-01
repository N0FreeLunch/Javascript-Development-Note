## maxBy
> Takes a function and two values, and returns whichever value produces the larger result when passed to the provided function.
- 두 개의 값을 받아 제공받은 함수를 통과한 결과 중 더 큰 값을 만들어 내는 결과를 반환한다.

> See also max, minBy.

## 설명
- 함수와 두 값을 받아, 두 값이 각각 주어진 함수의 인자로 할당되어 평가된 결과 값이 큰 값이 되는 쪽의 값을 인자로 전달한 두 값 중에서 반환한다.
- 첫 번째 인자로 두 번째 세 번째 인자로 받을 수 있는 타입과 동일한 타입의 인자를 받아 함수의 평가 값으로 순서를 비교할 수 있는 함수를 받는다.
- 두 번째 인자로 첫 번째 인자의 함수의 인자로 전달할 값을 받는다.
- 세 번째 인자로 첫 번째 인자의 함수의 인자로 전달할 값을 받는다.

## 표현
```
Ord b => (a → b) → a → a → a
```
- `Ord b =>` 순서가 있는 타입 b에 대해서
- `(a → b)` 첫 번째 인자로, 인자를 넣어서 순서를 서로 비교할 수 있는 값을 반환하는 함수를 받는다.
- `→ a →` 두 번째 인자로 첫 번째 인자로 받은 함수의 인자로 전달할 수 있는 값을 받는다.
- `→ a →` 세 번째 인자로도 첫 번째 인자로 받은 함수의 인자로 전달할 수 있는 값을 받는다.
- `→ a` 두 번째 인자와 세 번째 인자를 첫 번째 인자의 함수로 전달했을 때 반환하는 결과 값을 비교해서 더 큰 수의 인자를 반환한다.

## 예제
```
//  square :: Number -> Number
const square = n => n * n;

R.maxBy(square, -3, 2); //=> -3

R.reduce(R.maxBy(square), 0, [3, -5, 4, 1, -2]); //=> -5
R.reduce(R.maxBy(square), 0, []); //=> 0
```
- `R.maxBy(square, -3, 2)` `square`는 인자로 수를 받아서 제곱을 하는 함수이다. `-3`과 `2`중에서 `square` 함수를 통과했을 때 더 큰 수가 되는 값을 반환하므로 `-3`을 반환한다.
- `R.reduce(R.maxBy(square), 0, [3, -5, 4, 1, -2])`에서 초기 값은 0이고 배열의 원소를 순회적용 하므로 `R.maxBy(square)(0, 3) = 3`이므로 3이 다음으로 전달된다. `R.maxBy(square)(3, -5) = -5`이므로 -5가 다음으로 전달된다. `R.maxBy(square)(-5, 4) = -5`이므로 `-5`가 다음으로 전달된다. `R.maxBy(square)(-5, 1) = -5`이므로 `-5`가 다음으로 전달된다. `R.maxBy(square)(-5, -2) = -5`이므로 최종적으로 `-5`가 나온다.
- `R.reduce(R.maxBy(square), 0, [])`에서 초기 값은 0이고 배열에서 적용될 원소가 없으므로 `R.maxBy(square)`에 아무것도 적용하지 않고 초기값 0이 반환된다.

## Reference
- https://ramdajs.com/docs/#maxBy
