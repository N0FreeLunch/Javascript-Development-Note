## addIndex
> Creates a new list iteration function from an existing one by adding two new parameters to its callback function: the current index, and the entire list.

> This would turn, for instance, R.map function into one that more closely resembles Array.prototype.map. Note that this will only work for functions in which the iteration callback function is the first parameter, and where the list is the last parameter. (This latter might be unimportant if the list parameter is not used.)

## 설명
- 리스트를 순회(iteration) 할 때 콜백 함수의 인자에 index라는 파라메터를 추가하는 람다함수를 만든다.
- map 함수를 예를 들어 설명 하자. 
- 자바스크립트의 array.map() 배열 함수인 map을 쓰면 첫 번째 콜백으로 배열의 원소 (element), 두 번째 콜백으로 배열의 인덱스(index)를 하나씩 받는다. 
- RamdaJS의 map은 콜백 함수의 인자로 원소만을 가질 뿐 인덱스를 가지고 있지 않다. 이 map 함수를 사용할 때 콜백 함수의 인자로 리스트의 원소 뿐만 아니라 인덱스도 포함하여 받을 수 있도록 한다.
- RamdaJS의 기본 람다 함수에는 콜백에 인덱스를 기본적으로 포함하지 않고 리스트의 원소만 포함하고 있기 때문에 addIndex는 유용하다.

## 표현
```
(((a …) → b) … → [a] → *) → (((a …, Int, [a]) → b) … → [a] → *)
```
- `(((a …) → b) … → [a] → *) →` 부분을 보면 `((a …) → b)` 여러개의 인자를 받아서 단일한 결과값을 반환하는 형태의 함수를 `((a …) → b) …` 여러개 받고 마지막으로 `→ [a] →` 배열을 받아 `→ *` 어떤 결과값을 반환하는 함수를 받는다.
- `→ (((a …, Int, [a]) → b) … → [a] → *)`

## 예시
```
const mapIndexed = R.addIndex(R.map);
mapIndexed((val, idx) => idx + '-' + val, ['f', 'o', 'o', 'b', 'a', 'r']);
//=> ['0-f', '1-o', '2-o', '3-b', '4-a', '5-r']
```
- `R.addIndex` 부분을 보면, 먼저는 `R.map`이란 함수를 받고, 그 다음으로 `(val, idx) => idx + '-' + val`이란 인자를 받았다.
- R.map이란 람다함수를 자바스크립트 기본 배열 함수처럼 원소와 인덱스를 콜백 함수로 가지는 함수를 만들고 싶다면 R.addIndex 함수를 사용해서 만들 수 있다.


## Reference
- https://ramdajs.com/docs/#addIndex
