## symmetricDifference
> Finds the set (i.e. no duplicates) of all elements contained in the first or second list, but not both.
- (중복이 없는) 집합을 (구성하는데 필요한 원소를) 찾는다. (이 집합의) 모든 원소는 첫 번째 리스트(의 원소)와 두 번째 (인자의) 리스트(의 원소)를 포함하지만 양쪽 (모두에 속한) 원소는 포함하지 않는다.

> See also symmetricDifferenceWith, difference, differenceWith.

### 설명
- 인자로 받은 두 리스트에서 중복된 값을 포함하지 않는 리스트를 반환한다.
- 반환 된 결과는 두 리스트의 중복된 값을 제거한 배열을 각각 만든 후 만들어진 첫 번째 리스트를 먼저 나열한 뒤 만들어진 두 번째 리스트를 나열한 결과를 반환한다.
- symmetric difference는 수학적인 용어로 교집합을 포함하지 않는 원소 집합을 반환한다.

### 표현
```
[*] → [*] → [*]
```
- `[*] →`: 첫 번째 인자로 배열을 받는다. 이 때 배열의 인자의 종류에 특별한 제한이 있지 않으며, 다양한 종류의 다른 타입을 포함할 수 있다.
- `→ [*] →`: 두 번째 인자로도 배열을 받는다. 마찬가지로 인자의 종류에 제한이 없다.
- `→ [*]`: 첫 번째 인자와 첫 번째 원소를 나열한 후 두 번째 원소를 나열한다. 이 때 두 리스트에서 교집합에 해당하는 원소는 나열하지 않는다.

### 예제
```js
R.symmetricDifference([1,2,3,4], [7,6,5,4,3]); //=> [1,2,7,6,5]
R.symmetricDifference([7,6,5,4,3], [1,2,3,4]); //=> [7,6,5,1,2]
```
- `R.symmetricDifference([1,2,3,4], [7,6,5,4,3])` : 두 리스트의 교집합은 `[3,4]`이다. 첫 번째 리스트에서 교집합에 해당하는 값을 뺀 나머지 `[1,2]`와 두 번째 리스트에서 교집합에 해당하는 값을 뺀 나머지 `[7,6,5]`의 원소를 차례로 나열한 값인 `[1,2,7,6,5]`를 반환한다.
- `R.symmetricDifference([7,6,5,4,3], [1,2,3,4])` : 두 리스트의 교집합은 `[3,4]`이다. 첫 번째 리스트에서 교집합에 해당하는 값을 뺀 나머지 `[7,6,5]`와 두 번째 리스트에서 교집합에 해당하는 값을 뺀 나머지 `[1,2]`의 원소를 차례로 나열한 값인 `[7,6,5,1,2]`를 반환한다.

## Reference
- https://ramdajs.com/docs/#symmetricDifference