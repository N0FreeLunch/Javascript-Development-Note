## dropLastWhile
> Returns a new list excluding all the tailing elements of a given list which satisfy the supplied predicate function. It passes each value from the right to the supplied predicate function, skipping elements until the predicate function returns a falsy value. The predicate function is applied to one argument: (value).

## 표현
```
(a → Boolean) → [a] → [a]
(a → Boolean) → String → String
```
- 첫 번째 인자로 술어함수를 받는다.
- 두 번째 인자로 배열에 상당하는 대상을 받는다. 배열 또는 자바스크립트에서 배열처럼 접근할 수 있는 문자열을 받는다.
- 배열의 뒤에서 부터 술어 함수를 만족하지 않는 원소가 나올 때까지 제거한 결과를 반환한다. 두 번째 인자로 주어진 배열 또는 배열에 상당하는 문자열 타입과 동일한 타입을 반환한다.

## 설명
- 첫 번째 인자로 하나의 인자를 받는 술어 함수를 받는다.
- 두 번째 인자로 배열 또는 문자열을 받는다.
- 두 번째 인자로 받은 배열 또는 문자열의 뒤의 원소부터 차례로 첫 번째 인자에 할당한 술어함수의 인자에 넣어 평가하여 거짓이 나올 때 까지 계속한다.
- 거짓이 나오기 전의 모든 원소를 제거한 결과를 반환한다.

## 예제
```
const lteThree = x => x <= 3;

R.dropLastWhile(lteThree, [1, 2, 3, 4, 3, 2, 1]); //=> [1, 2, 3, 4]

R.dropLastWhile(x => x !== 'd' , 'Ramda'); //=> 'Ramd'
```
- `[1, 2, 3, 4, 3, 2, 1]` 배열의 뒤에서 부터 원소를 하나씩 `lteThree` 함수의 인자로 할당하고 참이 나오면 계속 제외하고 거짓이 나오면 제외하는 것을 멈춘다.
- `lteThree`는 3이하의 값인지 판단하는 술어함수이다. 주어진 배열의 뒤에서 부터 `1`, `2`, `3`은 주어진 술어 함수를 만족하는데 4번째인 `4`는 술어함수를 만족하지 못하므로 `[1, 2, 3, 4, 3, 2, 1]`에서 `[3, 2, 1]`을 제거한 `[1, 2, 3, 4]`만을 반환한다.
- `R.dropLastWhile(x => x !== 'd' , 'Ramda');` 뒤에서 부터 각 문자를 차례로 술어함수에 넣었을 때 `d`가 나오면 술어함수가 만족되지 못하므로 `d` 전까지인 마지막 `a`만 제거하여 `'Ramd'`란 결과를 반환한다.

## Reference
- https://ramdajs.com/docs/#dropLastWhile
