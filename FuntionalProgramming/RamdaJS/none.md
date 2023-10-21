## none
> Returns true if no elements of the list match the predicate, false otherwise.
- 주어진 리스트에서 주어진 술어 함수를 만족하는 원소가 하나도 매칭되지 않는다면 참을 반환하고 그렇지 않으면 거짓을 반환한다.

> Dispatches to the all method of the second argument, if present.

> Acts as a transducer if a transformer is given in list position.

## 설명
- 주어진 리스트의 원소들 중에 아무것도(none) 술어함수를 만족하는 것이 없을 때 참을 반환한다.

## 표현
```
(a → Boolean) → [a] → Boolean
```
- 첫 번째 인자로 참 거짓을 판단하는 술어 함수를 받는다.
- 두 번째 인자로 배열을 받는데, 배열의 원소는 첫 번째 인자의 술어 함수의 인자로 전달 가능한 대상이어야 한다.
- 만약 주어진 술어 함수를 만족하는 원소가 배열에 하나도 없으면 true를 반환하고 그렇지 않으면 false를 반환한다.

## 예제
```
const isEven = n => n % 2 === 0;
const isOdd = n => n % 2 !== 0;

R.none(isEven, [1, 3, 5, 7, 9, 11]); //=> true
R.none(isOdd, [1, 3, 5, 7, 8, 11]); //=> false
```
- `isEven`은 주어진 값이 짝수인지 판단하는 술어함수이며, `isOdd`는 주어진 값이 홀수인지 판단하는 술어함수이다.
- `[1, 3, 5, 7, 9, 11]`는 주어진 배열의 원소 중에 함께 할당된 술어함수 `isEven`를 만족하는 짝수가 없기 때문에 `true`를 반환한다.
- `[1, 3, 5, 7, 8, 11]`는 주어진 배열의 원소 중에 함께 할당된 술어함수 `isOdd`를 만족하는 홀수가 존재하므로 `false`를 반환한다.

## Reference
- https://ramdajs.com/docs/#none
