## dropRepeats
> Returns a new list without any consecutively repeating elements. 
- 연속적으로 반복하는 어떠한 원소도 없는 새로운 리스트를 반환한다.
> R.equals is used to determine equality.
- `R.equals` 함수는 동일성을 결정하는데 사용된다.
> Acts as a transducer if a transformer is given in list position.

## 표현
```
[a] → [a]
```
- 배열을 받아서 동일한 연속된 동일 원소를 제거한 배열을 반환한다.

## 설명
- 연속적으로 반복되는 원소를 제거한 결과를 반환한다.

## 예제
```
R.dropRepeats([1, 1, 1, 2, 3, 4, 4, 2, 2]); //=> [1, 2, 3, 4, 2]
```
- `1, 1, 1` 1이 연속되므로 하나만 남기고, `4, 4`도 연속되므로 하나만 남긴다. `2, 2`도 연속되므로 하나만 남긴다. 따라서 결과는 `[1, 2, 3, 4, 2]`이다.

## Reference
- https://ramdajs.com/docs/#dropRepeats
