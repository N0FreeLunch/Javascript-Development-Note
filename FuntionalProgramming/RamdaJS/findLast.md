## findLast
> Returns the last element of the list which matches the predicate, or undefined if no element matches.

> Acts as a transducer if a transformer is given in list position.

## 표현
```
(a → Boolean) → [a] → a | undefined
```
- `(a → Boolean) →` 
- `→ [a] →` 
- `→ a | undefined` 

## 설명
- find 함수와 닮은 기능을 제공한다. 단 주어진 리스트의 원소를 뒤에서 부터 순차적으로 순회하여 탐색한다.
- 첫 번째 인자로 술어함수를 받는다.
- 두 번째 인자로 첫 번째 인자의 술어함수의 인자로 할당될 수 있는 값을 원소로 한 배열을 받는다.
- 배열을 마지막 인덱스 부터 순차적으로 탐색하여 술어함수를 만족하는 함수를 발견하면 해당 원소를 반환하고 배열 전체를 순회해도 발견하지 못하면 undefined를 반환한다.

## 예제
```
const xs = [{a: 1, b: 0}, {a:1, b: 1}];
R.findLast(R.propEq('a', 1))(xs); //=> {a: 1, b: 1}
R.findLast(R.propEq('a', 4))(xs); //=> undefined
```
- `R.propEq('a', 1)`는 인자로 오브젝트를 받아서 오브젝트의 `a`프로퍼티의 값이 `1`이면 참을 아니면 거짓을 반환하는 술어함수이다.
- 배열의 원소를 뒤에서 부터 순차적으로 주어진 술어함수에 할당하여 보면 `{a:1, b: 1}`를 매칭하므로 순회를 종료하고 `{a:1, b: 1}`를 반환한다.
- `R.propEq('a', 4)`는 인자로 오브젝트를 받아서 오브젝트의 `a`프로퍼티의 값이 `4`이면 참을 아니면 거짓을 반환하는 술어함수이다.
- 배열의 원소를 뒤에서 부터 순차적으로 순회하여도 매칭되는 원소가 없으므로 undefined를 반환한다.

## Reference
- https://ramdajs.com/docs/#findLast
