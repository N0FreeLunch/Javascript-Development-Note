## dropRepeats
> Returns a new list without any consecutively repeating elements. 
- 연속적으로 반복하는 어떠한 원소도 없는 새로운 리스트를 반환한다.
> R.equals is used to determine equality.
- `R.equals` 함수는 동일성을 결정하는데 사용된다.
> Acts as a transducer if a transformer is given in list position.
- 리스트 위치에 변형기가 주어지면 변환기로 작동한다.
> See also [transduce](./transduce.md).

## 설명
- 연속적으로 반복되는 원소를 제거한 결과를 반환한다.

## 문법

```
R.dropRepeats(list): Array
```

- `list`: The array to consider.
- `list`: 논할 배열
- Returns Array `list` without repeating elements.
- 어떠한 반복되는 원소도 없는 배열인 `list`를 반환한다. 

## 표현
```
[a] → [a]
```
- `[a] →`: 배열을 인자로 받는다. 이 배열은 동일한 종류의 원소이다.
- `→ [a]`: 연속되고 반복되는 원소가 제거된 배열을 반환한다.

## 예제
```js
R.dropRepeats([1, 1, 1, 2, 3, 4, 4, 2, 2]); //=> [1, 2, 3, 4, 2]
```
- `1, 1, 1` 1이 연속되므로 하나만 남기고, `4, 4`도 연속되므로 하나만 남긴다. `2, 2`도 연속되므로 하나만 남긴다. 따라서 결과는 `[1, 2, 3, 4, 2]`이다.

## References
- https://ramdajs.com/docs/#dropRepeats
- https://github.com/ramda/ramda/blob/master/test/dropRepeats.js
- https://github.com/ramda/types/blob/develop/types/dropRepeats.d.ts
