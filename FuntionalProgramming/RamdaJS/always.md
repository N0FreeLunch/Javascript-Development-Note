## always
- R.always()
- 다른 언어나 라이브러리에서 const, constant, or K (for K combinator)로 표현함

## 설명
- 함수를 평가하기 전에 인자로 넣은 값을 함수를 평가할 때 반환하는 함수

## 표현
```
a → (* → a)
```
- `a → ` 임의의 단일 값을 인자로 받고
- `→ (* → a)` 함수를 반환하는데 반환된 함수 `(* → a)`는 `* →` 임의의 값을 넣었을 때 항상 `a →` `→ a`

## 예제
```
const t = R.always('Tee');
t(); //=> 'Tee'
```
- 'Tee' 라는 문자열을 인자로 집어 넣으면 `t` 함수를 평가할 때 항상 'Tee'를 반환함

## Reference
- https://ramdajs.com/docs/#always
