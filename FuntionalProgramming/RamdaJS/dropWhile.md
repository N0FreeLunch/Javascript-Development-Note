## dropWhile
> Returns a new list excluding the leading elements of a given list which satisfy the supplied predicate function. It passes each value to the supplied predicate function, skipping elements while the predicate function returns true. The predicate function is applied to one argument: (value).

> Dispatches to the dropWhile method of the second argument, if present.

> Acts as a transducer if a transformer is given in list position.

## 표현
```
(a → Boolean) → [a] → [a]
(a → Boolean) → String → String
```
- `(a → Boolean) → ` 첫 번째 인자로 술어 함수를 받는다.
- `→ [a] →`, `→ String →` 두 번째 인자로 배열에 상당하는 타입을 넣으며 배열의 원소는 첫 번째 인자의 술어함수가 받는 인자와 동일한 타입이다.
- `→ [a]`, `→ String` 배열에서 술어함수를 만족하지 않는 원소가 나올 때까지 왼쪽에서 부터 제거한 배열(배열 상당의 문자열)을 반환한다.

## 설명
- dropLastWhileList가 뒤에서 부터 술어 함수를 만족하지 않는 원소가 나올 때까지의 원소를 제거한 반면 dropWhile는 술어함수를 만족하지 않는 원소가 나올 때까지 주어진 배열의 앞에서 부터 제거한다.
- 첫 번째 인자로는 배열의 원소를 하나씩 넣어서 참이면 제거하도록 조건을 갖는 술어함수를 넣는다.
- 두 번째 인자로는 동일한 타입의 원소가 나열된 배열을 넣는다. 동일한 타입의 원소여야 첫 번째 인자의 함수에 할당할 수 있다. 두 번째 인자로는 배열에 상당하는 문자열도 넣을 수 있다.

## 예제
```
const lteTwo = x => x <= 2;

R.dropWhile(lteTwo, [1, 2, 3, 4, 3, 2, 1]); //=> [3, 4, 3, 2, 1]

R.dropWhile(x => x !== 'd' , 'Ramda'); //=> 'da'
```
- 첫 번째 인자인 `lteTwo`는 2이하의 수를 인자로 넣으면 참을 반환하는 함수이다.
- 두 번째 인자는 배열을 넣고 첫 번째 원소인 1은 2이하이므로 술어 함수를 만족하므로 제거한다. 두 번째 원소인 2는 2이하이므로 술어함수를 만족하므로 제거한다. 세 번째 원소인 3은 술어함수를 만족하지 못하므로 두 번째 원소까지 제거한 결과를 반환하여 `[3, 4, 3, 2, 1]`가 된다.
- `R.dropWhile(x => x !== 'd' , 'Ramda')`는 d가 나올 때까지 d 앞의 원소를 제거하므로 `da`가 반환된다.


## Reference
- https://ramdajs.com/docs/#dropWhile
