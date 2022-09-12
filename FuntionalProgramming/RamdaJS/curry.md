## Curry
> Returns a curried equivalent of the provided function. 
- 제공된 함수의 역할을 대신할 수 있는 커리된 함수를 반환한다.
> The curried function has two unusual capabilities. 
- 커리된 함수는 두 가지의 특별한 특징을 갖는다.
> First, its arguments needn't be provided one at a time. 
- 첫 번째로, 인자를 한 번에 모두 할당할 필요가 없다는 것이다.
> If `f` is a ternary function and g is `R.curry(f)`, the following are equivalent:
- 만약 함수 `f`가 세 개의 인자를 받는 함수라면, `R.curry(f)`인 함수 `g`의 다음 표현은 모두 같은 결과를 갖는다.
> - g(1)(2)(3) 
> - g(1)(2, 3) 
> - g(1, 2)(3) 
> - g(1, 2, 3)

> Secondly, the special placeholder value `R.__` may be used to specify "gaps", 
- 두 번째로, `R.__`라는 특별한 플레이스 홀더는 특별한 갭을 형성하는데 사용된다.
> allowing partial application of any combination of arguments, regardless of their positions. 
- 이 갭은 인자의 위치에 관계 없이 인자를 배치할 수 있도록 도와준다.
> If `g` is as above and `_` is `R.__`, the following are equivalent:
- `_`를 `R.__`이라고 할 때, 함수 `g`의 다음 표현은 모두 같은 결과를 같는다.
> - g(1, 2, 3)
> - g(_, 2, 3)(1)
> - g(_, _, 3)(1)(2)
> - g(_, _, 3)(1, 2)
> - g(_, 2)(1)(3)
> - g(_, 2)(1, 3)
> - g(_, 2)(_, 3)(1)

## 표현
```
(* → a) → (* → a)
```
- `(* → a) →` 여러 종류의 타입과 갯수의 인자를 받는 함수를 첫 번째 인자로 받는다.
- `→ (* → a)` 여러 종류의 타입과 개수의 인자를 받는 함수를 반환한다.

## 설명
- 함수의 인자를 여러 차례 나눠 받을 수 있는 함수로 만든다.
- 커링된 함수는 원본 함수가 받는 인자를 다 채우지 못할 경우 인자를 더 받을 수 있는 함수를 만든다.
- 커링된 함수는 원본 함수가 받아야 할 인자를 다 받을 경우 함수를 반환하지 않고 평가된 결과를 반환한다.
- 함수가 커링될 때 원본 함수를 변경하지 않고 커링된 새로운 함수를 만든다.
- 커링 된 함수가 원본 함수가 받아야 할 인자를 다 받지 못하게 되는 경우, 추가로 인자를 받을 수 있는 새로운 함수를 반환한다.

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
