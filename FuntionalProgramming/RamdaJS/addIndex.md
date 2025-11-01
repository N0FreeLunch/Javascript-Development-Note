## addIndex

> Creates a new list iteration function from an existing one by adding two new parameters to its callback function: the current index, and the entire list.
- 리스트의 순회에 사용되는 순회 함수를 기반으로 새로운 함수를 생성한다. (리스트의 원소 하나를 인자로 전달 받는) 기존 순회함수에 현재 (순회 함수에 전달할 원소의) 인덱스, 전체 리스트라는 파라머터를 콜백 함수에 추가한다.

> This would turn, for instance, R.map function into one that more closely resembles Array.prototype.map.
- 예를 들어 (리스트를 순회하면서 현재 순회 위치의 원소를 하나씩 콜백 함수에 전달하는) R.map 함수를 (원소, 인덱스, 전체 배열을 순회 함수를 콜백 함수에 전달하는) Array.prototype.map을 좀 더 닮은 (현재 원소, 인덱스, 전체 리스트를 콜백 함수에 전달하는) 함수로 바뀐다.

> Note that this will only work for functions in which the iteration callback function is the first parameter, and where the list is the last parameter. (This latter might be unimportant if the list parameter is not used.)
- 순회 콜백 함수를 첫 번째 파라메터로, 리스트는 마지막 파라메터로 하는 함수에 대해서만 동작한다. (리스트 파라메터가 사용되지 않으면 후자(리스트 파라메터)는 중요하지 않을 수도 있다.)

### 설명

- 콜백 함수를 첫 번째 인자로 받는 대상에 적용되는 함수로, 첫 번째 인자의 콜백함수에 인자를 전달할 때, 콜백 함수의 파라메터에 인덱스와 전체 리스트를 받을 수 있도록 파라메터를 추가하는 역할을 한다. RamdaJS에서 사용하는 콜백함수를 자바스크립트 네이티브의 배열의 콜백 함수처럼 원소, 인덱스, 전체 배열을 인자로 전달 받도록 구성하기 위해 사용한다.
- RamdaJS의 순회 함수를 콜백 함수로 받는 함수는 인덱스나 리스트 파라메터를 전달 받지 않고 원소만을 받도록 구성되어 있는 경우가 많다. map 함수를 예를 들면, 자바스크립트 네이티브 Array.prototype.map 배열 함수인 map을 쓰면 콜백 함수에 첫 번째 인자로 배열의 원소(element), 두 번째 인자로 배열의 인덱스(index), 세 번째 인자로 전체 리스트를 전달한다. RamdaJS의 map은 콜백 함수의 인자로 원소만을 가질 뿐 인덱스나 전체 리스트를 인자로 받지 않는다. addIndex는 콜백 함수의 인자로 리스트를 순회하고 있을 때의 원소 뿐만 아니라 인덱스 및 전체 배열을 전달 받을 수 있도록 한다.
- addIndex라는 이름은 배열에 새로운 원소를 추가하거나 기존 배열의 인덱스를 변경하는 등의 조작으로 오해하기 쉬운데, 배열을 변경하는 것이 아닌, 배열을 순회하는 콜백함수의 파라메터 사양을 바꾸기 위한 함수이다.

### 문법

```
R.addIndex(fn: Function): Function
```
> `fn`: A list iteration function that does not pass index or list to its callback
- `fn`: 리스트를 순회하는 함수를 하나 받는다. 이 함수는 콜백(함수)으로 (전체) 리스트나 인덱스를 전달하지 않는다. 
> Returns `function` An altered list iteration function that passes (item, index, list) to its callback
- `function`을 반환한다. 이 함수는 `(item, index, list)`을 콜백의 (인자로) 전달하는 리스트 순회 함수로 대체된다.

### 표현

```
(((a …) → b) … → [a] → *) → (((a …, Int, [a]) → b) … → [a] → *)
```
- `(((a …) → b) … → [a] → *) →`: `(((a …) → b) … → [a] → *)`이란 함수를 하나 받는다. 이 함수는 `((a …) → b)`와 같은 콜백함수를 받는다. 콜백 함수의 인자로는 `…`으로 여러 인자를 받을 수 있다. 콜백 함수 다음의 `… →`의 `…`는 콜백 함수를 첫 번째 인자로 받지만 다른 인자들도 갯수 제한 없이 추가로 받을 수 있다는 것을 의미한다. 마지막 인자로 `→ [a] →` 배열을 받는데, 배열을 받으면 평가가 이뤄지면서 특별한 종류 제한 없는 (`→ *`) 값을 반환한다.
- `→ (((a …, Int, [a]) → b) … → [a] → *)`: 첫 번째 인자의 조건에 맞는 함수를 넣었을 때 반환되는 함수로는 첫 번째로 받은 인자인 `(((a …) → b) … → [a] → *)`의 콟백함수 `((a …) → b)`에 addIndex에 적용한 함수를 하나 반환 하는데, 적용된 함수는 콜백함수로 `((a …, Int, [a]) → b)`형태의 함수를 받는다. 첫 번째 인자로 받은 함수의 콜백 함수가 받는 인자를 똑같이 받으면서 마지막 두 인자로 순회 대상의 인덱스(`Int`) 값과 순회 대상 전체 배열(`[a]`)을 인자로 추가로 받는 것을 알 수 있다. 콜백 함수 다음으로는 첫 번째 인자로 받은 함수와 동일하게 추가 인자(`…`)를 받을 수 있으며, 마지막으로 `→ [a] →` 전체 순회 대상 배열을 전달 받아 평가 된다. 마찬가지로 반환되는 값의 형태는 `→ *`으로 제한이 없다.

### 예시

```js
const mapIndexed = R.addIndex(R.map);
mapIndexed((val, idx) => idx + '-' + val, ['f', 'o', 'o', 'b', 'a', 'r']);
//=> ['0-f', '1-o', '2-o', '3-b', '4-a', '5-r']
```
- `R.addIndex` 부분을 보면, 먼저는 `R.map`이란 함수를 받았다. `map`함수의 첫번째 인자로 할당하는 콜백함수는 배열의 원소만을 전달 받는 함수이지만 `R.addIndex`가 적용된 `map` 함수는 첫 번째 인자로 배열의 원소뿐만 아니라 해당 원소의 인덱스 및 전체 배열을 전달하는 콜백 함수를 받을 수 있다. 따라서 `mapIndexed` 함수에는 `(val, idx) => idx + '-' + val`라는 콜백 함수를 넣고 `idx`란 추가 인덱스를 매개변수로 전달 받는다. `['f', 'o', 'o', 'b', 'a', 'r']`란 배열을 받아서 `R.map`과 동일한 형태의 결과를 반환 하므로 `(0, f) => 0 + '-' + 'f'`, `(1, o) => 1 + '-' + 'o'`, `(2, o) => 2 + '-' + 'o'`, `(3, b) => 3 + '-' + 'b'`, `(4, a) => 4 + '-' + 'a'`, `(5, r) => 5 + '-' + 'r'`이 각각의 순회에서 반환되고 이를 배열로 한 `['0-f', '1-o', '2-o', '3-b', '4-a', '5-r']`가 반환된다.
- R.map이란 람다함수를 자바스크립트 기본 배열 함수처럼 원소와 인덱스를 콜백 함수로 가지는 함수를 만들고 싶다면 R.addIndex 함수를 사용해서 만들 수 있다.

## References

- https://ramdajs.com/docs/#addIndex
- https://github.com/ramda/ramda/blob/master/test/addIndex.js
- https://github.com/ramda/types/blob/develop/types/addIndex.d.ts
