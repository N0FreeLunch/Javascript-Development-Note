## splitWhen
> Takes a list and a predicate and returns a pair of lists with the following properties:
- 리스트와 술어함수를 하나씩 받아서 다음 특징을 따르는 리스트의 쌍을 반환한다.

> - the result of concatenating the two output lists is equivalent to the input list;
- 출력된 두 리스트를 합친(concatenating) 결과는 주어진 리스트와 동등하다(equivalent).
> - none of the elements of the first output list satisfies the predicate; and
- (두 리스트가 출력이 되지만 그 중) 첫 번째로 출력된 리스트는 어느 원소도 주어진 술어함수를 만족하지 않는다. (왜냐하면, 술어함수를 만족하는 원소부터 다른 출력 그룹이 되기 때문이다.)
> - if the second output list is non-empty, its first element satisfies the predicate.
- 만약 두 번째로 출력된 리스트가 빈 값이 아니라면, (두 번째 출력 리스트의) 첫 번째 원소는 술어 함수를 만족한다. (왜냐하면, 술어함수를 만족하는 원소부터 두 번째 그룹으로 분류되기 때문이다.)

### 설명
- 리스트의 원소가 나열된 순서대로 주어진 술어함수를 적용하여 첫 번째로 참이 되는 부분부터 다른 그룹으로 분류하여 그 이전의 원소 그룹(술어함수가 거짓인 대상들)과 술어함수를 만족하는 원소를 포함한 그 이후의 원소 그룹으로 나눈다.

### 표현
```
(a → Boolean) → [a] → [[a], [a]]
```
- `(a → Boolean) →`: 첫 번째 인자로는 술어함수를 받는다. 타입 파라메터는 a인데 두 번째로 받는 배열의 원소를 전달 받으므로 동일한 타입 파라메터를 가진다.
- `→ [a] →`: 두 번째 인자로는 원소의 타입 파라메터가 a인 리스트를 받는다. 이 리스트는 첫 번째로 받는 술어함수의 인자로 전달될 수 있어야 한다.
- `→ [[a], [a]]`: 리스트를 분류하여 두 부분 집합을 만들기 때문에 두 번째 인자 `[a]`의 부분집합 `[a], [a]`가 되고, 함수의 반환값은 하나의 값이 되어야 하므로 배열로 묶어서 `[[a], [a]]`를 결과로 반환한다.

### 예제
```js
R.splitWhen(R.equals(2), [1, 2, 3, 1, 2, 3]);   //=> [[1], [2, 3, 1, 2, 3]]
```
- `R.equals(2)`는 인자를 하나 받아서 받은 인자의 값이 2와 같은지를 확인하는 술어함수이다.
- `[1, 2, 3, 1, 2, 3]`에서 첫 번째로 2가 나오는 부분은 인덱스 번호 1인 2이다. 술어함수를 만족하기 전까지의 인자 리스트 `[1]`과 술어함수를 만족하는 원소부터 나머지의 인자 리스트인 `[2, 3, 1, 2, 3]`를 묶으면 `[[1], [2, 3, 1, 2, 3]]`가 된다.

## Reference
- https://ramdajs.com/docs/#splitWhen
