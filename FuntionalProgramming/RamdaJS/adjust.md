## adjust
> Applies a function to the value at the given index of an array, returning a new copy of the array with the element at the given index replaced with the result of the function application.

## 설명
- 리스트의 특정한 원소를 지정해서 해당 원소를 변화 시키고자 할 때 사용한다.
- 배열에서 지정한 인데스의 원소에 주어진 함수를 적용하여 값을 변경한 새 배열을 반환한다.
- 여러 원소를 변경시키는 것이 아니라 단일 원소를 변경시킨다.

## 문법
```
R.adjust(indexNumber, callbackFunction, array)
```
반환타입 : `array`

## 표현
```
Number → (a → a) → [a] → [a]
```
- `Number →` 첫 번째 인자로는 인덱스 번호를 지정한다.
- `→ (a → a) →` 두 번째 인자로는 배열의 지정한 원소를 인자로 넣었을 때 치환하고 싶은 값을 리턴하는 함수를 받는다.
- `→ [a] →` 세 번째 인자로는 배열을 받는다.
- `→ [a]` 세 번째 인자로 받은 배열의 복사본이면서 첫 번째 인자로 받은 인덱스에 해당하는 원소를 두 번째 인자로 받은 함수의 인자로 넣었을 때 반환되는 값으로 원소를 치환한 배열을 반환한다.

## 예시
```
R.adjust(1, R.toUpper, ['a', 'b', 'c', 'd']);      //=> ['a', 'B', 'c', 'd']
R.adjust(-1, R.toUpper, ['a', 'b', 'c', 'd']);     //=> ['a', 'b', 'c', 'D']
```

## Reference
- https://ramdajs.com/docs/#adjust
