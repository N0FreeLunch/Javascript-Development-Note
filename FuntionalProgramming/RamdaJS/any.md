## any
- `R.any(predicate, list)`

## 설명
- `R.any(술어함수)(리스트);`
- 리스트의 원소들이 하나라도 주어진 술어함수를 만족하는지 확인하는 함수

## 표현
```
(a → Boolean) → [a] → Boolean
```
- `(a → Boolean)` 술어 함수를 첫 번째 인자로 받는다
- `→ [a]` 리스트를 두 번째 인자로 받는다
- `[a] → Boolean` 리스트의 어느 한 원소라도 술어 함수를 만족시키면 결과 값의 참 거짓을 반환한다.

## 예제
```
const lessThan0 = R.flip(R.lt)(0);
const lessThan2 = R.flip(R.lt)(2);
R.any(lessThan0)([1, 2]); //=> false
R.any(lessThan2)([1, 2]); //=> true
```
- `R.lt`은 첫 번째 인자 보다 두 번째 인자가 클 때 true를 반환
- `R.flip` 주어진 술어 함수의 첫번째 인자와 두 번째 인자의 순서를 바꾼다.
- `R.flip(R.lt)`의 의미는 첫 번째 인자가 두 번째 인자보다 작을 때 true를 반환
- `lessThan0`는 `R.flip(R.lt)(0)`으로 첫번째 인자인 0보다 다음으로 들어올 두 번째 인자 보다 작은지 판단
- `lessThan2`는 `R.flip(R.lt)(2)`으로 첫번째 인자인 2보다 다음으로 들어올 두 번째 인자 보다 작은지 판단
- `R.any(lessThan0)` 리스트로 받은 인자에서 0보다 작은 원소가 있는지 판단
- `R.any(lessThan2)` 리스트로 받은 인자에서 2보다 작은 원소가 있는지 판단

## Reference
- https://ramdajs.com/docs/#any
