# functor

> 1. u['fantasy-land/map'](a => a) is equivalent to u (identity)
- `u['fantasy-land/map'](a => a)`은 u와 같다. (항등함수)
> 3. u['fantasy-land/map'](x => f(g(x))) is equivalent to u['fantasy-land/map'](g)['fantasy-land/map'](f) (composition)
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
    - f가 함수가 아니면, fantasy-land/map의 동작은 결정되지 않는다.
    > 2. f can return any value.
    - f는 어떠한 값이든 반환할 수 있다.
    > 3. No parts of f's return value should be checked.
    - f의 반환 값 중 어떤 부분도 검사되면 안 된다.
2. fantasy-land/map must return a value of the same Functor
- fantasy-land/map은 반드시 같은 펑터의 값을 반환한다.
