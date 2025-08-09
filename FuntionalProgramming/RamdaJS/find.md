## find

> Returns the first element of the list which matches the predicate, or undefined if no element matches.
- 주어진 리스트에서 주어진 술어 함수를 만족하는 첫 번째 원소를 반환한다. 또는 술어함수를 만족하는 원소가 없는 경우에는 `undefined`를 반환한다.
> Dispatches to the find method of the second argument, if present.
- 주어진 리스트의 원소가 자기 순번이 되면 탐색함수에 두 번째 인자로 넣는다.
> Acts as a transducer if a transformer is given in list position.
- 리스트 위치에 변형기가(transformer) 주어지면 변환기(transducer)로 행동한다.
> See also [transduce](./transduce.md).

## 설명

- 첫 번째 인자로 술어함수를 받는다.
- 두 번째 인자로 첫 번째 인자의 술어함수의 인자로 할당될 수 있는 값을 원소로 한 배열을 받는다.
- 배열을 0번째 인덱스 부터 순차적으로 탐색하여 술어함수를 만족하는 함수를 발견하면 해당 원소를 반환하고 배열 전체를 순회해도 발견하지 못하면 undefined를 반환한다.

## 문법

```
R.find(fn, list): Object|undefined
```
> `fn`: The predicate function used to determine if the element is the desired one.
- `fn`: 원하는 원소를 결정하는데 사용되는 술어함수
> `list`: The array to consider.
- `list`: 고려될 배열
> Returns Object The element found, or `undefined`.
- 발견된 원소의 오브젝트 또는 `undefined`를 반환한다.

## 표현

```
(a → Boolean) → [a] → a | undefined
```
- `(a → Boolean) →`: 인자를 하나 받아서 참 거짓을 반환하는 술어 함수를 받는다.
- `→ [a] →`: 첫 번째 인자의 술어함수의 인자로 할당 될 수 있는 값을 원소로 한 배열을 받는다.
- `→ a | undefined`: 배열에서 술어함수를 만족하는 원소를 순차적으로 확인하고 만족하는 대상이 나오면 대항 원소를 반환하고 그렇지 않으면 undefined를 반환한다.

## 예제

```js
const xs = [{a: 1}, {a: 2}, {a: 3}];
R.find(R.propEq('a', 2))(xs); //=> {a: 2}
R.find(R.propEq('a', 4))(xs); //=> undefined
```
- `R.propEq('a', 2)`는 오브젝트를 인자로 받아서 `a` 프로퍼티의 값이 `2`이면 참을 반환 아니면 거짓을 반환하는 술어함수이다.
- `R.find`의 두 번째 원소는 오브젝트가 원소로 한 배열을 받았다. 오브젝트를 순회하여 `{a: 1}`는 거짓이므로 다음 원소를 확인하고 `{a: 2}`는 참이므로 `{a: 2}`를 반환한다.
- `R.propEq('a', 4)`는 `a` 프로퍼티의 값이 `4`인지 확인하는 술어함수이며 술어함수를 만족하는 원소가 없으므로 `undefined`를 반환한다.

## References
- https://ramdajs.com/docs/#find
- https://github.com/ramda/ramda/blob/master/test/find.js
- https://github.com/ramda/types/blob/develop/types/find.d.ts
