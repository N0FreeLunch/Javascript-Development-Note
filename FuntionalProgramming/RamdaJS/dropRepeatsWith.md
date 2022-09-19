## dropRepeatsWith
> Returns a new list without any consecutively repeating elements. Equality is determined by applying the supplied predicate to each pair of consecutive elements. The first element in a series of equal elements will be preserved.

> Acts as a transducer if a transformer is given in list position.

## 표현
```
((a, a) → Boolean) → [a] → [a]
```
- `((a, a) → Boolean) →` 두 인자를 받는 술어함수를 받는다.
- `→ [a] → ` 두 번째 인자로는 첫 번째 인자의 술어 함수의 인자로 할당할 수 있는 원소를 갖는 배열을 받는다.
- 배열 안의 연속한 원소에 대해 술어함수를 만족하는 대상을 제외한 원소만 남긴 배열을 반환한다.

## 설명
- 첫 번째 인자로 주어진 배열의 원소를 인자로 받을 수 있는 술어함수를 지정한다.
- 두 번째 인자로 배열을 받는다.
- 주어진 배열의 연속한 두 원소에 대해 연속되는 원소가 주어진 술어함수를 만족하는 경우 연속된 두 원소 중 두 번째 원소를 제거한 결과를 반환한다.

## 예제
```
const l = [1, -1, 1, 3, 4, -4, -4, -5, 5, 3, 3];
R.dropRepeatsWith(R.eqBy(Math.abs), l); //=> [1, 3, 4, -5, 3]
```
- `R.eqBy`함수는 첫 번째 인자로 함수를 받고 두 번째와 세 번째 인자는 첫 번째 인자로 받은 술어함수의 인자로 들어갈 값 둘을 받아 평가한 결과가 같은지 판단하는 함수이다.
- `R.eqBy(Math.abs)` 연속된 두 대상의 절대값이 같은지 확인하는 함수이다.
- `R.dropRepeatsWith` 함수는 배열의 두 원소를 하나씩 `R.eqBy(Math.abs)`함수에 넣고 다음 원소와 같은 값을 가지는지 확인한다.
- 엄밀히는 첫 번째 원소 `1`과 다음 원소 `-1`을 비교하고 일치하므로 tmp 배열에 넣지 않아 `1`만 남은 상태, 이 `1`과 1을 비교하고 일치하므로 tmp 배열에 넣지 않아 `1`만 남은 상태, 이 1과 3을 비교하고 일치하지 않으므로 tmp 배열에 3을 넣고 이 3과 4를 비교하고 일치하지 않으므로 4를 tmp에 넣고, 이 4와 -4를 비교하여 일치하므로 tmp 배열에 넣지 않는 방식으로 결국 tmp 배열에 담긴 값을 최종적으로 반환하는 방식이다.
- 간단하게 연속한 두 원소를 `R.eqBy(Math.abs)` 함수에 할당한 뒤 일치하면 두 번째 원소를 제거한다고 봐도 된다. `1, -1`에서 -1을 제거하고 1만 남은 이 1과 1을 비교하여 두 번째 1을 제거하여 1만 남음 1과 3을 비교하여 3을 남김, 3과 4를 비교하여 4를 남김 4와 -4를 비교하여 두 번째를 제거하여 4를 남김, 4와 -4를 비교하여 두 번째를 제거하여 4를 남김 이런식으로 해석을 해도 된다. 선언형이므로 함수 내부의 로직은 서로 다를 수 있지만 결과는 같다.

## Reference
- https://ramdajs.com/docs/#dropRepeatsWith
