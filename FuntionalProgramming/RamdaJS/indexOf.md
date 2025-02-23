## indexOf
> Returns the position of the first occurrence of an item in an array, or -1 if the item is not included in the array. R.equals is used to determine equality.
- 어떤 배열에 속한 아이템 중에서 첫번째로 나타난 아이템의 위치를 반환한다. 또는 해당 배열에 (찾고자 하는) 아이템이 포함되어 있지 않다면 -1을 반환한다. R.equals는 (찾고자 하는 원소와 배열에 포함된 원소의) 동등성을 결정하는데 사용한다.

열에서 항목이 처음 나타나는 위치를 반환하거나 항목이 배열에 포함되지 않은 경우 -1을 반환합니다. R.equals는 동등성을 결정하는 데 사용됩니다.

## 설명
- 첫 번째 인자로 찾을 값을 지정하고
- 두 번째 인자로 배열을 지정한다.
- 지정한 값이 주어진 배열의 원소 중에서 몇 번 인덱스에 위치해 있는지를 알려주는 인덱스 번호를 반환한다.
- 만약 지정한 값이 배열의 원소 중에 없다면 `-1`을 반환한다.
- 이 때 지정한 값과 배열의 원소의 일치를 확인하는 방법은 `R.equals`함수를 하여 참이면 일치하므로 인덱스 번호를 반환하고 거짓이면 일치하지 않으므로 다음 원소를 계속해서 확인한다.

## 문법

```
R.indexOf(target, xs): Number
```

> target: The item to find.
- target: 발견할 아이템
> xs: The array to search in.
- xs: 검색할 배열
> Returns Number the index of the target, or -1 if the target is not found.
- 대상의 인덱스 번호 또는 대상을 찾을 수 없다면 -1을 반환한다. 

## 표현
```
a → [a] → Number
```
- `a →`: 첫 번째 인자로 배열의 원소로 가능한 종류의 어떤 값을 받는다.
- `→ [a] →`: 두 번째 인자로 배열을 받는데 어떤 종류의 원소값을 갖는 배열을 받는다.
- `→ Number`: 첫 번째 인자로 받은 값과 주어진 배열의 원소가 일치하는 값이 있다면 해당 원소의 인덱스 번호를 반환한다.

## 예제
```js
R.indexOf(3, [1,2,3,4]); //=> 2
R.indexOf(10, [1,2,3,4]); //=> -1
```

## References
- https://ramdajs.com/docs/#indexOf
- https://github.com/ramda/ramda/blob/master/test/indexOf.js
- https://github.com/ramda/types/blob/develop/types/indexOf.d.ts
