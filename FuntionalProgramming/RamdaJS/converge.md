## converge


## 표현
```
((x1, x2, …) → z) → [((a, b, …) → x1), ((a, b, …) → x2), …] → (a → b → … → z)
```

## 설명


## 예제
```
const average = R.converge(R.divide, [R.sum, R.length])
average([1, 2, 3, 4, 5, 6, 7]) //=> 4

const strangeConcat = R.converge(R.concat, [R.toUpper, R.toLower])
strangeConcat("Yodel") //=> "YODELyodel"
```
- `R.divide`함수는 첫번째 인자로 피제수를 받고 두 번째 인자로 제수를 받아서 피제수/제수 연산한 결과를 반환하는 함수이다.
- `R.converge`를 사용하여 `R.divide` 함수에 인자를 직접할당하지 않고 첫 번째 인자는 배열의 첫 번째 함수의 결과를 두 번째 인자는 배열의 두 번째 함수의 결과를 받는 식으로 함수의 인자를 배열의 함수가 평가된 결과 값으로 할당하는 방식을 사용할 수 있게 한다. `R.converge(대상함수, [대상함수의 인자에 할당하기 위한 값을 만들 함수들])`이다.
- `[1, 2, 3, 4, 5, 6, 7]`이란 값이 주어지면, `R.sum([1, 2, 3, 4, 5, 6, 7])`의 결과가 `R.divide`의 첫 번째 인자로 할당되고, `R.length([1, 2, 3, 4, 5, 6, 7])`의 결과가 `R.divide`의 두 번째 인자로 할당된다.
- `R.concat`함수는 인자로 받은 두 배열형식의 타입을 가진 대상의 모든 원소가 들어 있는 하나의 배열로 합친 결과를 반환한다.
- `R.toUpper("Yodel")`의 결과가 `R.concat`의 첫 번째 인자로 할당되고, `R.toLower("Yodel")`의 결과가  `R.concat`의 두 번째 인자로 할당된다.
- 따라서 결과는 `R.concat("YODEL", "yodel")`인 `"YODELyodel"`가 된다.

## Reference
- https://ramdajs.com/docs/#converge
