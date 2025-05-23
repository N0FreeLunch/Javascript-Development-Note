## curryN

> Returns a curried equivalent of the provided function, with the specified arity. The curried function has two unusual capabilities. First, its arguments needn't be provided one at a time. If `g` is `R.curryN(3, f)`, the following are equivalent:
> - g(1)(2)(3)
> - g(1)(2, 3)
> - g(1, 2)(3)
> - g(1, 2, 3)

> Secondly, the special placeholder value `R.__` may be used to specify "gaps", allowing partial application of any combination of arguments, regardless of their positions. If `g` is as above and `_` is `R.__`, the following are equivalent:
> - g(1, 2, 3)
> - g(_, 2, 3)(1)
> - g(_, _, 3)(1)(2)
> - g(_, _, 3)(1, 2)
> - g(_, 2)(1)(3)
> - g(_, 2)(1, 3)
> - g(_, 2)(_, 3)(1)

### 설명

- `R.curry` 함수가 고정된 수의 인자를 받는 함수에 적용되어 고정된 수의 인자의 수가 다 차면 평가 되는 것과 달리 `R.curryN`은 가변 인자를 받는 함수에 적용되어 지정한 수의 인자를 받으면 함수를 평가하는 방식으로 되어 있다.

### 문법

```
R.curryN(length, fn): function
```

> `length`: The arity for the returned function.
- `length`: 반환된 함수의 인자의 수 (arity).
> `fn`: The function to curry.
- `fn`: 커링할 대상 함수
> Returns function A new, curried function.
- 새로운 커링된 함수를 반환한다.

### 표현

```
Number → (* → a) → (* → a)
```
- `Number →`: 몇 개의 인자를 받아서 커링한 함수를 평가할 것인지를 정한다.
- ` → (* → a) →`: 커링할 대상 함수를 받는다. 임의의 종류와 인자의 수를 가지며(`*`) 특정한 종류(`a`)를 반환하는 함수를 받는다.
- `→ (* → a)`: 두 번째 인자로 받은 함수와 동일한 인자와 반환 값을 갖지만, 평가 되기에 충분한 인자를 받지 않으면 인자를 나눠 받을 수 있는 커링된 함수가 반환 된다.

### 예제

```js
const sumArgs = (...args) => R.sum(args);

const curriedAddFourNumbers = R.curryN(4, sumArgs);
const f = curriedAddFourNumbers(1, 2);
const g = f(3);
g(4); //=> 10
```
- `R.sum`은 수가 든 배열을 인자로 받아 배열 안의 모든 수를 더한 결과를 반환하는 함수이다.
- `(...args) => R.sum(args)`는 가변 인자를 받아서 가변인자를 배열로 할당한다는 의미를 가지고 있다.
- `R.curryN(4, sumArgs)`는 가변 인자로 받는 인자를 4개로 설정하고 `sumArgs`함수를 실행한다는 의미를 갖는다.
- `curriedAddFourNumbers(1, 2)`에서 인자를 두 개 할당, `f(3)`에서 인자를 하나 할당, `g(4)`에서 인자를 하나의 인자를 할당하여 총 4개의 인자를 할당하고 나서 함수 내부의 `R.sum(args)`를 평가한 결과를 반환한다.


### References
- https://ramdajs.com/docs/#curryN
- https://github.com/ramda/ramda/blob/master/test/curryN.js
- https://github.com/ramda/types/blob/develop/types/curryN.d.ts
