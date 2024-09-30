## always
> Returns a function that always returns the given value.
- 항상 주어진 값을 반환하는 함수를 반환한다.

> Note that for non-primitives the value returned is a reference to the original value.
- 원시값이 아닌 값이 반환되는 경우 원본 값을 참조한다.

> This function is known as const, constant, or K (for K combinator) in other languages and libraries.
- 이 함수는 다른 언어나 라이브러리에서 const, constant, K (for K combinator)로 알려져 있다.

## 설명
- 인자로 주어진 값을 반환하는 함수를 반환한다. 반환된 함수는 어떠한 인자를 받든 항상 always 함수에 주어진 첫번째 인자를 반환한다.

## 문법
```
always(val): function
```
- val : The value to wrap in a function
- Returns function A Function :: * -> val.

## 표현
```
a → (* → a)
```
- `a → `: 임의의 단일 값을 인자로 받고
- `→ (* → a)`: 함수를 반환하는데 반환된 함수 `(* → a)`는 `* →` 임의의 값을 넣었을 때 항상 앞서 인자로 지정한 값인 `a →`의 값을 함수의 평가 값 `→ a` 으로 반환된다.

## 예제
```js
const t = R.always('Tee');
t(); //=> 'Tee'
```
- 'Tee' 라는 문자열을 인자로 집어 넣으면 `t` 함수를 평가할 때 항상 'Tee'를 반환한다.

## References
- https://ramdajs.com/docs/#always
- https://github.com/ramda/ramda/blob/master/test/always.js
- https://github.com/ramda/types/blob/develop/types/always.d.ts
