## dropWhile
> Returns a new list excluding the leading elements of a given list which satisfy the supplied predicate function.
- 주어진 술어 함수를 만족하는 주어진 리스트의 원소들의 이끄는 원소 (첫 번째 원소부터 차례로 이어지는)를 제외한 새로운 리스트를 반환한다.
> It passes each value to the supplied predicate function, skipping elements while the predicate function returns true.
- 주어진 술어 함수에 (순회에 따른 원소인) 각각의 값을 전달하고, 순회 합수가 true를 반환할 때까지 계속된다.
> The predicate function is applied to one argument: (value).
- 술어 함수는 하나의 인자만 지원한다. 술어 함수(로 전달되는) 인자를 value라고 하자.
> Dispatches to the dropWhile method of the second argument, if present.
- 두 번째 인자의 (원소에) dropWhile이란 메소드가 있으면 dropWhile 메소드를 실행한다.
> Acts as a transducer if a transformer is given in list position.
- 변형기가 리스트 위치에 주어지면, 변환기로 동작한다.

## 설명

- dropLastWhileList가 뒤에서 부터 술어 함수를 만족하지 않는 원소가 나올 때까지의 원소를 제거한 반면, dropWhile는 술어함수를 만족하지 않는 원소가 나올 때까지 주어진 배열의 앞에서 부터 제거한다.
- 첫 번째 인자로는 배열의 원소를 하나씩 넣어서 참이면 제거하도록 조건을 갖는 술어함수를 넣는다.
- 두 번째 인자로는 동일한 타입의 원소가 나열된 배열을 넣는다. 동일한 타입의 원소여야 첫 번째 인자의 함수에 할당할 수 있다. 두 번째 인자로는 배열에 상당하는 문자열도 넣을 수 있다.

## 표현

```
(a → Boolean) → [a] → [a]
(a → Boolean) → String → String
```
- `(a → Boolean) → `: 첫 번째 인자로 술어 함수를 받는다.
- `→ [a] →`, `→ String →`: 두 번째 인자로 배열에 상당하는 타입을 넣으며 배열의 원소는 첫 번째 인자의 술어함수가 받는 인자와 동일한 타입이다.
- `→ [a]`, `→ String`: 배열에서 술어함수를 만족하지 않는 원소가 나올 때까지 왼쪽에서 부터 제거한 배열(배열 상당의 문자열)을 반환한다.

## 문법

```
R.dropWhile(fn, xs): Array
```
> `fn`: The function called per iteration.
- `fn`: 순회의 반복마다 호출되는 함수
> `xs`: The collection to iterate over.
- `xs`: 순회할 콜렉션
> Returns Array A new array.
- 새로운 배열을 반환한다.

## 예제

```js
const lteTwo = x => x <= 2;

R.dropWhile(lteTwo, [1, 2, 3, 4, 3, 2, 1]); //=> [3, 4, 3, 2, 1]

R.dropWhile(x => x !== 'd' , 'Ramda'); //=> 'da'
```
- 첫 번째 인자인 `lteTwo`는 2이하의 수를 인자로 넣으면 참을 반환하는 함수이다.
- 두 번째 인자는 배열을 넣고 첫 번째 원소인 1은 2이하이므로 술어 함수를 만족하므로 제거한다. 두 번째 원소인 2는 2이하이므로 술어함수를 만족하므로 제거한다. 세 번째 원소인 3은 술어함수를 만족하지 못하므로 두 번째 원소까지 제거한 결과를 반환하여 `[3, 4, 3, 2, 1]`가 된다.
- `R.dropWhile(x => x !== 'd' , 'Ramda')`는 d가 나올 때까지 d 앞의 원소를 제거하므로 `da`가 반환된다.

## References
- https://ramdajs.com/docs/#dropWhile
- https://github.com/ramda/ramda/blob/master/test/dropWhile.js
- https://github.com/ramda/types/blob/develop/types/dropWhile.d.ts
