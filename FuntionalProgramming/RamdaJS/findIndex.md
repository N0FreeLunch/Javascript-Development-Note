## findIndex

> Returns the index of the first element of the list which matches the predicate, or -1 if no element matches.
- 술어 함수에 매치하는 리스트의 첫 번째 원소 인덱스를 반환한다. 만약 (술어함수에 매칭되는) 원소가 없다면 -1을 반환한다.
> Acts as a transducer if a transformer is given in list position.
- 만약 변형기가 리스트 위치에 주어지면 변환기로서 작용한다.

## 설명

- `find`가 주어진 술어함수를 만족하는 원소를 반환한 것에 반해 `findIndex`는 원소를 반환하지 않고 주어진 리스트의 몇번 인덱스인지 반환한다.
- 첫 번째 인자로 배열에서 탐색을 위한 술어함수를 받는다.
- 두 번째 인자로 첫 번째 인자의 술어함수의 인자로 할당할 수 있는 원소로 이루어진 리스트를 받는다.
- 리스트의 원소를 첫 번째부터 순차적으로 순회하여 원소를 첫 번째 인자로 할당한 술어함수의 인자에 할당하여 참이 나오면 해당원소의 인덱스 번호를 반환하고 순회를 멈춘다.
- 주어진 리스트에 술어함수를 만족하는 원소가 없는 경우 `-1`을 반환한다.

## 문법

```
R.findIndex(fn, list): Number
```
> `fn`: The predicate function used to determine if the element is the desired one.
- `fn`: 이 술어함수는 원하는 원소를 판별하기 위해 사용된다.
> `list`: The array to consider.
- `list`: (원소를 찾기 위한 더미로) 고려할 배열
> Returns Number The index of the element found, or `-1`.
- Number 타입의 값을 반환한다. 원소를 찾으면 해당 (원소의) 인덱스를 찾지 못하면 -1을 반환한다.

## 표현

```
(a → Boolean) → [a] → Number
```
- `(a → Boolean) → `: 술어 함수를 받는다.
- `→ [a] →`: 술어함수의 인자와 동일한 타입의 원소로 구성된 배열을 받는다.
- `→ Number`: 배열의 원소를 순차적으로 탐색해 매칭되는 인덱스 번호를 반환하며 매칭되지 않는다면 `-1`을 반환하므로 Number 타입으로 반환된다.

## 예제

```
const xs = [{a: 1}, {a: 2}, {a: 3}];
R.findIndex(R.propEq('a', 2))(xs); //=> 1
R.findIndex(R.propEq('a', 4))(xs); //=> -1
```
- `R.propEq('a', 2)` 함수는 오브젝트를 받아서 프로퍼티 `a`의 값인 `2`인지 확인하는 술어함수이다. 프로퍼티 `a`의 값이 `2`인 원소의 인덱스 번호는 `1`이므로 `1`을 반환한다.
- `R.propEq('a', 4)` 함수는 오브젝트를 받아서 프로퍼티 `a`의 값인 `4`인지 확인하는 술어함수이다. 프로퍼티 `a`의 값이 `4`인 원소는 주어진 배열에 존재하지 않는다. 따라서 `-1`을 반환한다.

## References

- https://ramdajs.com/docs/#findIndex
- https://github.com/ramda/ramda/blob/master/test/findIndex.js
- https://github.com/ramda/types/blob/develop/types/findIndex.d.ts
