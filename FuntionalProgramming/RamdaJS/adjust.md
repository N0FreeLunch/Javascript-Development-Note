## adjust
> Applies a function to the value at the given index of an array, returning a new copy of the array with the element at the given index replaced with the result of the function application.
- 배열의 주어진 인덱스에 해당하는 값을 함수에 적용한다. 주어진 인덱스가 함수의 적용 결과로 대체된 배열의 새로운 복사본을 반환한다.

## 설명
- 리스트의 특정한 원소를 지정해서 해당 원소를 변화 시키고자 할 때 사용한다.
- 배열에서 지정한 인데스의 원소를 주어진 함수를 적용하여 얻을 값으로 변경한 새 배열을 반환한다.
- 여러 원소를 변경시키는 것이 아니라 단일 원소를 변경시킨다.

## 문법
```
R.adjus(idx, fn, list): Array
```
- idx: The index.
- fn: The function to apply.
- list: An array-like object whose value at the supplied index will be replaced.
- Returns Array A copy of the supplied array-like object with the element at index `idx` replaced with the value returned by applying `fn` to the existing element.

## 표현
```
Number → (a → a) → [a] → [a]
```
- `Number →`: 첫 번째 인자로는 인덱스 번호를 지정한다.
- `→ (a → a) →`: 두 번째 인자로는 세 번째 인자로 받은 배열의 첫 번째 인자로 지정한 인덱스의 원소를 인자로 넣었을 때 치환하고 싶은 원소를 얻기 위한 함수를 받는다.
- `→ [a] →`: 세 번째 인자로는 배열을 받는다. 두 번째 인자로 받은 함수의 인자로 전달할 수 있는 종류(`a`)의 값을 원소로 갖는 배열이다.
- `→ [a]`: 세 번째 인자로 받은 배열의 복사본이면서 첫 번째 인자로 받은 인덱스에 해당하는 원소를 두 번째 인자로 받은 함수의 인자로 넣었을 때 반환되는 값으로 원소를 치환한 배열을 반환한다. 배열의 원소 종류(`a`)의 일관성을 위해서 대체된 값도 같은 종류의 값이 되어야 하므로 두 번째 인자의 함수의 반환값의 종류도 `a`가 된다.

## 예시
```js
R.adjust(1, R.toUpper, ['a', 'b', 'c', 'd']);      //=> ['a', 'B', 'c', 'd']
R.adjust(-1, R.toUpper, ['a', 'b', 'c', 'd']);     //=> ['a', 'b', 'c', 'D']
```
- `['a', 'b', 'c', 'd']`에서 1번 인덱스의 값을 `b`를 `R.toUpper` 함수에 전달한 결과인 `B`를 1번 인덱스와 교체한 배열을 반환한다. 따라서 `['a', 'B', 'c', 'd']`이다.
- `['a', 'b', 'c', 'd']`에서 -1번 인덱스의 값을 `d`를 `R.toUpper` 함수에 전달한 결과인 `D`를 -1번 인덱스와 교체한 배열을 반환한다. 따라서 `['a', 'b', 'c', 'D']`이다.

## Reference
- https://ramdajs.com/docs/#adjust
- https://github.com/ramda/ramda/blob/master/test/adjust.js
- https://github.com/ramda/types/blob/develop/types/adjust.d.ts
