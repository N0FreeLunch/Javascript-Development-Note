## all
> Returns true if all elements of the list match the predicate, false if there are any that don't.

> Dispatches to the all method of the second argument, if present.

> Acts as a transducer if a transformer is given in list position.

## 설명
- 술어 함수와 리스트를 인자로 받아서, 리스트 내의 모든 원소가 주어진 술어 함수를 만족하는지 확인하고 모든 함수가 주어진 술어 함수를 만족하면 true, 주어진 술어 함수를 만족하지 않으면 false를 반환한다. 

## 문법
```
R.all(predicate, list)
```
- predicate는 술어 함수를 의미하며, 대상의 참 거짓을 판별할 때 사용한다. predicate 부분에는 리스트 원소의 참 거짓을 판별할 수 있는 콜백함수를 정의한다.

## 표현
```
(a → Boolean) → [a] → Boolean
```
- `(a → Boolean)` 첫 번째 인자로는 어떤 인자에 대한 참/거짓을 판별하는, 곧 Boolean을 반환하는 함수를 인자로 받는다.
- `[a]` 두 번째 인자로는 배열을 받는다. 이 배열의 원소는 첫 번째 인자로 받은 함수의 인자로 할당 가능한 유형이어야 한다.
- 최종적으로 리스트의 각 원소에 대한 전체의 참/거짓을 판별하는 Boolean을 반환한다.

## 예시
```
const equals3 = R.equals(3);
R.all(equals3)([3, 3, 3, 3]); //=> true
R.all(equals3)([3, 3, 1, 3]); //=> false
```
- `equals3`은 값이 3인지 판별하는 함수
- `R.all(equals3)`은 리스트를 받아서 리스트의 원소가 모두 3인지에 대한 참/거짓을 판별하는 함수
- `R.all(equals3)`에 `([3, 3, 1, 3])` 리스트를 넣어서 함수를 평가하여 참 거짓을 판단한 결과를 얻는다.

## Reference
- https://ramdajs.com/docs/#all
