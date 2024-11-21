## R.count

> Returns the number of items in a given `list` matching the predicate `f`
- 주어진 `list`에서 술어함수 `f`에 매칭되는 아이템의 수를 반환한다.

### 설명

- 배열의 원소를 주어진 술어함수에 하나씩 전달하여 술어함수를 만족하는 배열의 원소를 수를 반환한다.
- 첫 번째 인자로 참 거짓을 구분하는 술어 함수를 받는다.
- 두 번째 인자로 첫 번째 인자인 술어함수의 인자로 할당될 수 있는 대상 리스트를 받는다.
- 두 번째 인자의 리스트에서 첫 번째 인자의 술어함수를 만족하는 대상의 갯수를 반환한다.

### 문법

```
R.count(f, list): Number
```
> `f`: predicate to match items against
- `f`: (리스트의) 아이템을 매칭하기 위하 술어함수
> `list`: The list to count elements from
- `list`: (리스트의 매칭되는) 원소의 수를 카운트하기 위한 리스트
> Return Number the count of items matching the predicate
- 술어함수에 매칭되는 아이템의 수를 Number으로 반환 한다.

### 표현

```
(a → Boolean) → [a] → Number
```
- 첫 번째 인자로는 술어함수(`(a → Boolean)`)를 받는다.
- 두 번째 인자로는 술어함수의 인자로 할당될 수 있는 타입을 원소로 갖는 배열을 받는다.
- 결과는 술어함수를 만족하는 배열 원소의 갯수이다.

### 예제

```
const even = x => x % 2 == 0;

R.count(even, [1, 2, 3, 4, 5]); // => 2
R.map(R.count(even), [[1, 1, 1], [2, 3, 4, 5], [6]]); // => [0, 2, 1]
```
- `even` 함수는 짝수인 경우 참을 반환하고 그렇지 않으면 거짓을 반환하는 매칭 조건이다.
- `R.count`는 주어진 조건 함수를 만족하는 값을 `[1, 2, 3, 4, 5]`에서 찾아서 만족하는 값의 갯수를 반환한다.
- `R.map`은 주어진 리스트의 각각의 원소를 인자로 하여 `R.count(even)` 함수로 평가한 결과를 배열로 받는다.
- `[1, 1, 1]`에서 짝수를 만족하는 값의 갯수는 0, `[2, 3, 4, 5]`에서 짝수를 만족하는 값의 갯수는 2, `[6]`애서 짝수를 만족하는 값의 갯수는 1이므로 결과는 `[0, 2, 1]`가 된다.

## References
- https://ramdajs.com/docs/#count
- https://github.com/ramda/ramda/blob/master/test/count.js
- https://github.com/ramda/types/blob/develop/types/count.d.ts
