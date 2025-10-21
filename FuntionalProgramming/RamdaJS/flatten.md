## flatten

> Returns a new list by pulling every item out of it (and all its sub-arrays) and putting them in a new array, depth-first.
- 배열 내의 모든 아이템을 하위 배열에서 꺼내고 꺼낸 것들을 새로운 배열에 넣어 새로운 리스트를 반환한다. 반환된 배열의 깊이는 1이다.

> See also [unnest](./unnest.md).

## 설명

- 배열 안에 원소로 배열이 들어가 있거나 중첩된 모든 배열의 원소들을 꺼내어, 원소가 배열 또는 배열을 포함하고 있는 배열을 원소로 가지지 않도록 가장 바깥 배열을 제외하고는 내부 원소를 꺼내 모두 가장 바깥 배열의 배열이 아닌 원소가 되도록 한다.

## 문법

```
R.flatten(list: Array): Array
```
> `list`: The array to consider.
- `list`: 고려할 배열
> Returns Array The flattened list.
- 평탄화된 리스트 배열을 반환한다.

## 표현

```
[a] → [b]
```
- `[a] →`: 첫 번째 인자로 배열을 받으며 원소로 중첩된 배열을 받을 수 있다.
- `→ [b]`: 배열 원소 또는 배열 원소의 내부 중첩이 해제된 배열을 반환한다.

## 예제

```js
R.flatten([1, 2, [3, 4], 5, [6, [7, 8, [9, [10, 11], 12]]]]);
//=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
```
- `1, 2, [3, 4], 5, [6, [7, 8, [9, [10, 11], 12]]]]`애서 `[3, 4]`의 원소를 꺼내어 `1, 2, 3, 4, 5, [6, [7, 8, [9, [10, 11], 12]]]]`
- `[6, [7, 8, [9, [10, 11], 12]]]]`애서 `6`을 꺼내어 `1, 2, 3, 4, 5, 6, [7, 8, [9, [10, 11], 12]]]`
- `[7, 8, [9, [10, 11], 12]]]`에서 7, 8을 꺼내어 `1, 2, 3, 4, 5, 6, 7, 8, [9, [10, 11], 12]`
- `[9, [10, 11], 12]`에서 9를 꺼내어 `1, 2, 3, 4, 5, 6, 7, 8, 9, [10, 11], 12`
- `[10, 11]`에서 10, 11을 꺼내어 `1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12`가 되도록 한다.

## References

- https://ramdajs.com/docs/#flatten
- https://github.com/ramda/ramda/blob/master/test/flatten.js
- https://github.com/ramda/types/blob/develop/types/flatten.d.ts
