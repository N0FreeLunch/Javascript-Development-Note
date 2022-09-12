## Curry
> Returns a curried equivalent of the provided function. The curried function has two unusual capabilities. First, its arguments needn't be provided one at a time. If `f` is a ternary function and g is `R.curry(f)`, the following are equivalent:
> Secondly, the special placeholder value `R.__` may be used to specify "gaps", allowing partial application of any combination of arguments, regardless of their positions. If g is as above and `_` is `R.__`, the following are equivalent:

## 표현
```
(* → a) → (* → a)
```

## 설명


## 예제
```
const addFourNumbers = (a, b, c, d) => a + b + c + d;

const curriedAddFourNumbers = R.curry(addFourNumbers);
const f = curriedAddFourNumbers(1, 2);
const g = f(3);
g(4); //=> 10
```
- `addFourNumbers`함수를 `R.curry` 함수의 인자로 할당하고 `curriedAddFourNumbers` 함수를 반환한다.
- `curriedAddFourNumbers` 함수는 원래 4개의 인자를 받는 함수였으나, 두 개의 인자를 받아서 내부에 보존하고 나머지 두 개의 인자를 받는 함수를 반환한다.
- 함수 `f`는 2개의 인자를 가지고 있고 내부적으로 `addFourNumbers` 함수를 평가하기 위한 두 개의 추가로 받는다.
- `R.curry`를 사용하면 추가로 받아야 할 인자를 하나씩 받을 수 있으며 원래 받아야 할 인자인 4개의 인자가 채워지지 않으면 추가로 인자를 받을 수 있는 새로운 함수를 반환한다.
- `f(3)`은 총 4개 받아야 하는 인자 중 3개를 받은 형태이며 함수 `g`는 마지막 인자를 받는 함수가 된다.

## Reference
- https://ramdajs.com/docs/#curry
