## all
> Returns true if all elements of the list match the predicate, false if there are any that don't.
- 만약 리스트의 모든 원소들이 술어함수에 매칭되면 true를 반환하고 어떤 원소라도 술어함수를 매칭하지 못하면 false를 반환한다.

> Dispatches to the all method of the second argument, if present.
- 두 번째 인자에 all 메소드가 존재하는 경우 all 메소드를 발동한다.

> Acts as a transducer if a transformer is given in list position.
- 만약 transformer가 list 위치에 주어지면 변환기(transducer)로서 행동한다.

## 설명
- 술어 함수와 리스트를 인자로 받아서, 리스트 내의 모든 원소가 주어진 술어 함수를 만족하는지 확인하고 모든 함수가 주어진 술어 함수를 만족하면 true, 그렇지 않으면 false를 반환한다.

## 문법
```
R.all(fn: (T) => Boolean, list: array<T>): Boolean
```
- predicate: The predicate function.
- list: The array to consider.
- Returns Boolean `true` if the predicate is satisfied by every element, `false` otherwise.

## 표현
```
(a → Boolean) → [a] → Boolean
```
- `(a → Boolean)`: 첫 번째 인자로는 어떤 인자에 대한 참/거짓을 판별하는 술어함수를 받는다. 두 번째 인자로 받은 배열의 원소와 동일한 종류(`a`)의 값을 받는다.
- `[a]`: 두 번째 인자로는 배열을 받는다. 이 배열의 원소는 첫 번째 인자로 받은 함수의 인자로 할당 가능한 종류(`a`)이어야 한다.
- `→ Boolean`: 최종적으로 리스트의 각 원소에 대한 전체의 참/거짓을 판별하는 Boolean을 반환한다.

## 예시
```js
const equals3 = R.equals(3);
R.all(equals3)([3, 3, 3, 3]); //=> true
R.all(equals3)([3, 3, 1, 3]); //=> false
```
- `equals3`은 값이 3인지 판별하는 함수
- `R.all(equals3)`은 리스트를 받아서 리스트의 원소가 모두 3인지에 대한 참/거짓을 판별하는 함수
- `R.all(equals3)`에 `([3, 3, 1, 3])` 리스트를 넣어서 함수를 평가하여 참 거짓을 판단한 결과를 얻는다.

## Reference
- https://ramdajs.com/docs/#all
- https://github.com/ramda/ramda/blob/master/test/all.js
- https://github.com/ramda/types/blob/develop/types/all.d.ts
