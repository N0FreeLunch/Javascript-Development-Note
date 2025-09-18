## findLastIndex

> Returns the index of the last element of the list which matches the predicate, or -1 if no element matches.
- 술어함수를 만족하는 리스트의 마지막 원소의 인덱스를 반환한다. 또는 (술어함수를 만족하는) 원소가 없다면 -1을 반환한다.
> Acts as a transducer if a transformer is given in list position.
- 만약 리스트 위치에 변형기(transformer)가 주어지면 변환기(transducer)로 동작한다.
> See also [transduce](./transduce.md), [lastIndexOf](./lastIndexOf.md).

## 설명
- `findLast`가 주어진 배열의 뒤에서 부터 순차적으로 원소를 순회하여 주어진 술어함수를 만족하는 원소를 반환한 것에 반해 `findLastIndex`는 원소를 반환하지 않고 주어진 리스트의 몇 번 인덱스인지 반환한다.
- 첫 번째 인자로 배열에서 탐색을 위한 술어함수를 받는다.
- 두 번째 인자로 첫 번째 인자의 술어함수의 인자로 할당할 수 있는 원소로 이루어진 리스트를 받는다.
- 리스트의 원소를 마지막 인덱스의 원소부터 순차적으로 순회하여 원소를 첫 번째 인자로 할당한 술어함수의 인자에 할당하여 참이 나오면 해당원소의 인덱스 번호를 반환하고 순회를 멈춘다.
- 주어진 리스트에 술어함수를 만족하는 원소가 없는 경우 `-1`을 반환한다.

## 문법

```
R.findLastIndex(fn, list): Number
```
> `fn`: The predicate function used to determine if the element is the desired one.
- `fn`: 원소가 원하는 것인지를 결정하기 위해 사용되는 술어함수
> `list`: The array to consider.
- `list`: 고려할 배열
> Returns Number The index of the element found, or `-1`.
- Number (타입)을 반환한다. (술어함수에 의해) 찾은 원소의 인덱스 번호 또는 (발견하지 못했다면) -1을 반환한다.

## 표현

```
(a → Boolean) → [a] → Number
```
- `(a → Boolean) → `: 술어 함수를 받는다.
- `→ [a] →`: 술어함수의 인자로 전달할 수 있는 종류의 원소로 구성된 배열을 받는다.
- `→ Number`: 배열의 원소를 마지막 인덱스의 원소부터 순차적으로 탐색해 매칭되는 인덱스 번호를 반환하며 매칭되지 않는다면 `-1`을 반환하므로 Number 타입으로 반환된다.

## 예제

```js
const xs = [{a: 1, b: 0}, {a:1, b: 1}];
R.findLastIndex(R.propEq('a', 1))(xs); //=> 1
R.findLastIndex(R.propEq('a', 4))(xs); //=> -1
```

- `R.propEq('a', 1)`는 인자로 오브젝트를 받아서 오브젝트의 `a`프로퍼티의 값이 `1`이면 참을 아니면 거짓을 반환하는 술어함수이다.
- 배열의 원소를 뒤에서 부터 순차적으로 주어진 술어함수에 할당하여 보면 `{a:1, b: 1}`를 매칭하므로 순회를 종료하고 `{a:1, b: 1}`의 인덱스 번호인 `1`을 반환한다.
- `R.propEq('a', 4)`는 인자로 오브젝트를 받아서 오브젝트의 `a`프로퍼티의 값이 `4`이면 참을 아니면 거짓을 반환하는 술어함수이다.
- 배열의 원소를 뒤에서 부터 순차적으로 순회하여도 매칭되는 원소가 없으므로 `-1`을 반환한다.

## References

- https://ramdajs.com/docs/#findLastIndex
- https://github.com/ramda/ramda/blob/master/test/findLastIndex.js
- https://github.com/ramda/types/blob/develop/types/findLastIndex.d.ts
