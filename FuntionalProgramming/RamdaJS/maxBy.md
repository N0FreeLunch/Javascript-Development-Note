## maxBy
> Takes a function and two values, and returns whichever value produces the larger result when passed to the provided function.
- 두 개의 값을 받아 제공받은 함수를 통과한 결과 중 더 큰 값을 만들어 내는 결과를 반환한다.

> See also max, minBy.

## 설명

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


## Reference
- https://ramdajs.com/docs/#maxBy
