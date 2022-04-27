## sort

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
- 

## Reference
- https://ramdajs.com/docs/#sort
