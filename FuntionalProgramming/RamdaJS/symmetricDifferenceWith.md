## symmetricDifferenceWith
> Finds the set (i.e. no duplicates) of all elements contained in the first or second list, but not both. Duplication is determined according to the value returned by applying the supplied predicate to two list elements.
- 첫 번째 리스트와 두 번째 리으스에 포함된 모든 원소를 중복 없이 갖는 집합을 찾아낸다. (원소가 나열된 공간에서 어떤 조건을 만족하는 원소들의 그룹을 찾아낸다고 보면 된다.) 주어진 술어함수에 두 리스트의 원소를 전달한 결과 값에 따라 중복이 판별된다.

> See also symmetricDifference, difference, differenceWith.

### 설명
- symmetricDifference가 두 집합의 원소를 합쳤을 때 교집합의 원소를 배제하는 것과 달리, symmetricDifferenceWith는 두 집합의 원소를 합쳤을 때 각각의 원소 중 술어함수를 통과하는 대상이 되는 원소를 배제한다.
- 두 집합에서 메모리 상에서 동일한 값이 아니더라도 문법적으로 같은 값을 가지는 경우 술어함수에 전달한 결과 값이 동일하므로 그 결과 값이 참이 참인 경우양쪽 집합에서 원소가 배제된다.

### 표현
```
((a, a) → Boolean) → [a] → [a] → [a]
```
- `((a, a) → Boolean) →`: 첫 번째 인자로 술어함수를 받는다. 두 번째 세 번째 인자로 받는 배열의 원소를 각각 술어함수의 첫 번째 인자와 두 번째 인자로 전달 받으므로 두 배열의 원소 타입 파라메터인 `a`를 인자로 받는다.
- `→ [a] →`: 두 번째 인자로 배열을 받는다.
- `→ [a] →`: 세 번째 인자로 배열을 받는다. 두 번째 인자와 세 번째 인자의 타입파라메터는 `a`로 동일한데 이는 첫 번째 두 원소 값이 일치하는지 확인하기 위한 술어함수에 전달할 수 있는 값이어야 하기 때문이다.
- `→ [a]`: 두 집합의 합집합을 배열로 반환하되, 술어함수를 만족하는 원소는 제거된 배열을 반환한다.

### 예제
```js
const eqA = R.eqBy(R.prop('a'));
const l1 = [{a: 1}, {a: 2}, {a: 3}, {a: 4}];
const l2 = [{a: 3}, {a: 4}, {a: 5}, {a: 6}];
R.symmetricDifferenceWith(eqA, l1, l2); //=> [{a: 1}, {a: 2}, {a: 5}, {a: 6}]
```

## Reference
- https://ramdajs.com/docs/#symmetricDifferenceWith
