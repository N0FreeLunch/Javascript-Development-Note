## indexOf
> Returns the position of the first occurrence of an item in an array, or -1 if the item is not included in the array. R.equals is used to determine equality.

## 표현
```
a → [a] → Number
```
- `a →` 임의의 타입의 어떤 값을 받는다.
- `→ [a] →` 임의의 타입의 값을 원소로 하는 배열을 받는다.
- `→ Number` 첫 번째 인자로 받은 값과 주어진 배열의 원소가 일치하는 값이 있다면 해당 원소의 인덱스 번호를 반환한다.

## 설명
- 첫 번째 인자로 찾을 값을 지정하고
- 두 번째 인자로 배열을 지정한다.
- 지정한 값이 주어진 배열의 원소 중에서 몇 번 인덱스에 위치해 있는지를 알려주는 인덱스 번호를 반환한다.
- 만약 지정한 값이 배열의 원소 중에 없다면 `-1`을 반환한다.
- 이 때 지정한 값과 배열의 원소의 일치를 확인하는 방법은 `R.equals`함수를 하여 참이면 일치하므로 인덱스 번호를 반환하고 거짓이면 일치하지 않으므로 다음 원소를 계속해서 확인한다.

## 예제
```
R.indexOf(3, [1,2,3,4]); //=> 2
R.indexOf(10, [1,2,3,4]); //=> -1
```

## Reference
- https://ramdajs.com/docs/#indexOf
