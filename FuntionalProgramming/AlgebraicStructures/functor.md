# functor

> 1. `u['fantasy-land/map'](a => a)` is equivalent to u (identity)
- `u['fantasy-land/map'](a => a)`은 u와 같다. (항등함수)
> 3. `u['fantasy-land/map'](x => f(g(x)))` is equivalent to `u['fantasy-land/map'](g)['fantasy-land/map'](f)` (composition)
- `u['fantasy-land/map'](x => f(g(x)))`는 `u['fantasy-land/map'](g)['fantasy-land/map'](f)`와 같다. (컴포지션)

fantasy-land/map method
```
fantasy-land/map :: Functor f => f a ~> (a -> b) -> f b
```

> A value which has a Functor must provide a fantasy-land/map method. The fantasy-land/map method takes one argument:
- Functor를 갖는 값은 반드시 fantasy-land/map 메소드를 제공해야 한다. fantasy-land/map 메소드는 하나의 인자를 받는다.
```
u['fantasy-land/map'](f)
```

> 1. f must be a function,
- f는 반드시 함수여야 한다.
    > 1. If f is not a function, the behaviour of fantasy-land/map is unspecified.
    - f가 함수가 아니면, fantasy-land/map의 동작은 (어떻게 동작이 이뤄질지가) 결정되지 않는다.
    > 2. f can return any value.
    - f는 어떠한 값이든 반환할 수 있다.
    > 3. No parts of f's return value should be checked.
    - f의 반환 값 중 어떤 부분도 검사되면 안 된다.
2. fantasy-land/map must return a value of the same Functor
- fantasy-land/map은 반드시 같은 펑터의 값을 반환한다.

## 설명

functor는 범주와 범주 사이의 맵이다. 예를 들어 정의역(X)인 자연수와 공역(Y)인 자연수가 존재할 때 X의 원소 x, Y의 원소 y에 대해, 임의의 x에 대해 f(x) = y가 성립하면 연산 f에 대해 X->Y로의 functor라고 부를 수 있다. 함수 f가 `x+1`이면 정의역과 치역 사이의 매핑이 되기 때문에 펑터이다. 하지만 `x-1`이면 x가 0일 때 y가 -1이 되므로 자연수의 범위가 아니므로 펑터라고 할 수 없다. 정의역과 공역에 따라서 동일한 함수라도 펑터가 될 수도 있고 펑터가 되지 않을 수도 있다.

범주와 범주 사이의 값의 변환을 통해 하나의 범주의 값을 다른 범주의 값으로 만드는 것을 펑터라고 부른다. 한 범주(X)가 자연수이고 다른 범주(Y)가 음의 정수라고 할 때, 함수 f가 `-x`이면 펑터이지만, `-x+1`이면 x가 1인 경우 0이 되어 음의 정수 집합을 만족하지 않아 펑터가 되지 않는다.

동일 범주 안의 연산은 펑터라고 부르지는 않으며, 서로 다른 범주로의 값의 전환이 이뤄질 때 펑터라고 부른다. 그래서 펑터 F에 대해 F(f(g(x)))에서 `f(g(x))`는 범주의 이동이 없는 동일 범주 내의 연산이며, F가 적용 되었을 때 범주의 전환이 이뤄지는 것이다. F(g(x))F(f(x))는 `g(x)`와 `f(x)`는 동일 범주 내의 연산이며, F(g(x))는 다른 범주로의 값의 전환, F(f(x))는 다른 범주로의 값의 전환에 해당한다.

자바스크립트에서 펑터라는 것은 배열을 의미한다. 배열(펑터)에 map 함수를 사용해서 그 결과가 배열이 될 때 원소의 갯수의 변화가 없다면 이는 정의역의 값에 대한 치역의 값이 매칭되므로 펑터라고 할 수 있다.

`u['fantasy-land/map'](a => a)`: fantasy-land/map의 개념에서 성립하는 배열을 functor u라고 하자. 동일 범주 내 연산으로 항등함수(`a => a`)가 주어졌을 경우, 그 결과는 펑터 u와 같다는 의미이다. `R.map(a => a)`는 자바스크립트의 배열 u에 대해 `R.map(a => a, u)`은 `u`가 된다.

`u['fantasy-land/map'](x => f(g(x)))`: fantasy-land/map의 개념에서 성립하는 배열을 functor u라고 하자. 동일 범주 내 연산으로 합성함수(`x => f(g(x))`)가 주어졌을 경우, 그 결과는 `u['fantasy-land/map'](g)`로 반환된 펑터에 `['fantasy-land/map'](f)`를 전달한 것과 같다는 의미이다. 곧, `R.map(x => f(g(x)), u)`는 자바스크립트 배열에 대해 `R.pipe(R.map(x => g(x)), R.map(x => f(x)))(u)`와 같아야 한다는 것을 의미한다.
