## takeLastWhile
> Returns a new list containing the last n elements of a given list, passing each value to the supplied predicate function, and terminating when the predicate function returns false.
- 주어진 리스트에서 마지막에 위치한 n개의 원소를 포함한 새로운 리스트를 반환한다. 주어진 술어함수에 각각의 원소값을 전달하며, 술어함수의 반환값이 false가 되는 경우 종료된다.

> Excludes the element that caused the predicate function to fail.
- 술어함수를 실패하게 만드는 (false를 반환하도록 하는) 원소는 배제한다.

> The predicate function is passed one argument: (value).
- 술어 함수는 하나의 인자(value)를 전달 받는다.

> See also dropLastWhile, addIndex.

### 설명
- 주어진 집합의 원소들 중에서 나열되는 순서상 마지막에 위치하는 원소부터 차례로 술어함수에 전달하여 true를 반환하는 대상만을 갖는 집합을 반환한다. 이 때 반환된 집합의 원소의 나열되는 순서는 그대로 유지된다. 이 때 순서란 크기의 비교가 아닌 나열된 순서를 의미한다.

### 표현

#### 배열의 경우
```
(a → Boolean) → [a] → [a]
```
- `(a → Boolean) →`: 첫 번째 인자로 술어 함수를 받는다.
- `→ [a] →`: 두 번째 인자로 배열을 받는다. 배열의 원소는 모두 첫 번째 인자로 받은 술어함수의 인자로 전달할 수 있는 종류여야 한다.
- `→ [a]`: 술어함수를 통과한 원소만을 반환하므로 동일한 타입 파라메터 a의 값을 원소로 하는 배열을 반환한다.

#### 문자열의 경우
```
(a → Boolean) → String → String
```
- `(a → Boolean)`: 첫 번째 인자로 술어함수를 받는다. 이 때 a는 문자열의 문자를 받을 수 있는 종류이다.
- `→ String →`: 두 번째 인자로 문자열을 받는다.
- `→ String`: 두 번째 인자로 받은 문자열의 문자 중에서 마지막까지의 연속한 n개의 문자를 나열한 문자열을 반환한다.

### 예제
```js
const isNotOne = x => x !== 1;

R.takeLastWhile(isNotOne, [1, 2, 3, 4]); //=> [2, 3, 4]

R.takeLastWhile(x => x !== 'R' , 'Ramda'); //=> 'amda'
```
- `isNotOne`: 술어함수는 인자로 받은 값이 1이 아닌지를 확인한다.
- `R.takeLastWhile(isNotOne, [1, 2, 3, 4])`: 마지막 원소 부터 `isNotOne` 함수에 전달한 결과가 false가 나올 때 까지 차례로 순회할 때 true가 나오는 원소는 4, 3, 2이다. 원소의 나열 순서를 그대로 한 배열은 `[2, 3, 4]`가 된다.
- `R.takeLastWhile(x => x !== 'R' , 'Ramda')`: 마지막 문자부터 ` => x !== 'R'` 함수에 문자 하나씩 전달한 결과가 false가 나올 때 까지 차례로 순회할 때 true가 나오는 문자는 a, d, m, a이다. 원소의 나열 순서를 그대로 한 문자열은 `'amda'`가 된다.

## Reference
- https://ramdajs.com/docs/#takeLastWhile
