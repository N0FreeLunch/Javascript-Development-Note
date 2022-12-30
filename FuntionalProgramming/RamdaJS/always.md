## always
> Returns a function that always returns the given value. Note that for non-primitives the value returned is a reference to the original value.

> This function is known as const, constant, or K (for K combinator) in other languages and libraries.
- 이 함수는 다른 언어나 라이브러리에서 const, constant, K (for K combinator)로 알려져 있다.

## 설명
- always 함수의 인자로 인자로 넣은 값을 함수를 평가할 때 반환하는 함수

## 문법
```
(always(any))()
```
반환타입 : any로 할당한 값의 타입

반환값 : any로 할당한 값


## 표현
```
a → (* → a)
```
- `a → ` 임의의 단일 값을 인자로 받고
- `→ (* → a)` 함수를 반환하는데 반환된 함수 `(* → a)`는 `* →` 임의의 값을 넣었을 때 항상 앞서 인자로 지정한 값인 `a →`의 값을 함수의 평가 값 `→ a` 으로 반환

## 예제
```
const t = R.always('Tee');
t(); //=> 'Tee'
```
- 'Tee' 라는 문자열을 인자로 집어 넣으면 `t` 함수를 평가할 때 항상 'Tee'를 반환함

## Reference
- https://ramdajs.com/docs/#always
