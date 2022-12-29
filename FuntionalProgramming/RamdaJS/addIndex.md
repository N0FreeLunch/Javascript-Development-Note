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
- `(((a …) → b) … → [a] → *) →` 부분을 보면 `(((a …) → b) … → [a] → *)`이란 함수를 하나 받는다. 이 함수는 `((a …) → b)`와 같은 콜백함수를 받고, 콜백 함수 다음의 `…`는 콜백함수 뿐만 아니라 부가적으로 추가 인자를 여러 개 받을 수 있다는 의미이다. 또한 마지막 인자로 `→ [a] →` 배열을 받는다. 배열을 받으면 평가가 이뤄지면서 어떤 형태의 `→ *` 값을 반환하는 형태의 함수 `(((a …) → b) … → [a] → *)`이를 첫 번째 인자로 받는다.
- `→ (((a …, Int, [a]) → b) … → [a] → *)` 부분을 보면 첫 번째로 받은 인자인 `(((a …) → b) … → [a] → *)`를 addIndex에 적용한 함수를 하나 반환 하는데, 이 함수를 사용할 때는 첫 번째 인자로 `((a …, Int, [a]) → b)`라는 함수를 받고 추가 인자 `…`를 여러 개 받을 수 있으며 마지막으로 ` → [a] →` 배열을 하나 받아서 평가 되어 `→ *`의 결과 값을 얻게 된다. 이 때 `((a …, Int, [a]) → b)` 부분은 콜백함수인데 addIndex에의 첫 번째 인자로 받은 함수의 콜백함수인 `((a …) → b)`와 같이 `a …` 콜백함수에 전달 되는 값을 전달 받지만 `a …, Int, [a]` 정수인자와 배열인자도 추가로 전달 받는다. 정수 인자는 주어진 배열`→ [a] →`의 인덱스이며 배열 인자는 배열 전체 `→ [a] →`의 배열을 그래도 전달 받을 수 있는 기능을 제공한다.

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
