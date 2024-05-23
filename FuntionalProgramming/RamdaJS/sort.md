## sort
> Returns a copy of the list, sorted according to the comparator function, which should accept two values at a time and return a negative number if the first value is smaller, a positive number if it's larger, and zero if they are equal. Please note that this is a copy of the list. It does not modify the original.
- 리스트의 복사본을 반환한다. 비교 함수(comparator function)에 의한 순서대로 정렬을 하며, 비교함수는 한 번에 두 개의 값을 받으며 만약 첫 번째 값이 두 번째 값 보다 작으면 음수를 반환하고, 첫 번째 값이 두 번째 값 보다 크면 양수를 반환한다. 첫 번째 값과 두 번째 값이 같으면 0을 반환한다. 리스트의 (원소를 직접 변경한 값이 아닌) 복사본임에 주의하자. sort 함수는 (리스트) 원본을 바꿀 수는 없다.

> See also ascend, descend.

## 설명
- 연속된 두 값을 순서대로 비교함수에 전달했을 때, 앞의 값에서 뒤의 값을 뺀 결과가 음수이면 순서는 그대로이고 양수이면 순서는 바뀐다. 이 때 빼기 연산의 자리에 비교 함수가 들어갔을 때 반환되는 값이 음수이면 순서는 그대로이고 양수이면 순서가 바뀌는 정렬을 한다.
- `a > b` 인 경우는 `a - b > 0`이며, `a = b` 인 경우는 `a - b = 0`이며, `a < b`인 경우는 `a - b < 0`이다.
- `a > b`는 b 보다 a가 더 크다라는 의미이므로 순서를 b, a로 나열한다.
- `a = b`는 같으므로 순서를 그대로 둔다.
- `a < b`는 a 보다 b가 더 크므로 a, b 순서로 나열한다.
- 첫 번째 인자는 비교를 위한 함수를 넣는다. sort 함수의 두 번째 인자로 받는 배열의 원소를 순차적으로 적용하여 비교한다.

## 표현
```
((a, a) → Number) → [a] → [a]
```
- `(a, a) → Number` 연산 가능한 동일 타입의 인자를 두 개를 받아서 연산 결과를 수(Number)로 반환하는 함수를 받는다.
- `→ [a] →` 그리고 '첫번째 인자에 할당한 함수'의 인자 타입과 동일한 타입을 원소로 갖는 배열을 받는다.
- `→ [a]` 배열의 원소들이 `((a, a) → Number)`에 따라 정렬된 배열을 결과로 받는다.

## 예제
```
const diff = function(a, b) { return a - b; };
R.sort(diff, [4,2,7,5]); //=> [2, 4, 5, 7]
```
- `diff`는 비교 함수이다. 비교 방식이 `a - b`이므로 `a - b > 0`일 경우에만 b, a 순서로 한다.
- 먼저 `4,2`를 받아서 `4 - 2 > 0`이므로 `2, 4` 순서로 순서를 바꾼다.
- 다음으로 `2, 4`의 4와 `[4,2,7,5]`의 7을 받아서 `4 - 7 < 0`이므로 `4, 7` 순서로 그대로 한다.
- 다음으로 `4, 7`의 7과 `[4,2,7,5]`의 5를 받아서 `7 - 5 > 0`이므로 `5, 7` 순서로 순서를 바꾼다.
- 따라서 결과는 `[2, 4, 5, 7]`이다.

## Reference
- https://ramdajs.com/docs/#sort
