## either

> A function wrapping calls to the two functions in an || operation, returning the result of the first function if it is truth-y and the result of the second function otherwise.
- 두 함수에 대한 호출(calls)을 || 연산으로 래핑하는 함수로, 참(에 상당하는 값)이면 첫 번째 함수의 결과를 반환하고 그렇지 않으면 (거짓에 상당하는 값이면) 두 번째 함수의 결과를 반환한다.
> Note that this is short-circuited, meaning that the second function will not be invoked if the first returns a truth-y value.
- 이것은 짧은 순환으로서, 두 번째 함수는 첫 번째 함수가 참(에 상당하는) 값을 반환하는 경우에, 두 번째 함수는 실행되지 않는다.
> In addition to functions, R.either also accepts any fantasy-land compatible applicative functor.
- 함수를 적용할 때, `R.either`는 어떠한 fantasy-land 호환으로 적용되는 펑터를 받을 수 있다.

## 설명

두 술어함수를 받아서 술어함수의 결과를 || 연산자로 연결한다. 술어 함수의 반환 값은 불리언이고, '첫 번째 술어 함수의 반환된 불리언 값' || '두 번째 술어함수의 반환된 불리언 값'으로 구성된다.

## 문법

```
R.either(f, g): Fucntion 
```
> `f`: a predicate
- `f`: 어떤 술어함수
> `g`: another predicate
- `g`: 다른 술어 함수
> Returns function a function that applies its arguments to `f` and `g` and `||`s their outputs together.
- 

## 표현

```
(*… → Boolean) → (*… → Boolean) → (*… → Boolean)
```
- `(*… → Boolean) →`: 첫 번째 인자로 술어 함수를 받는다.
- `→ (*… → Boolean) →`: 두 번째 인자로 술어 함수를 받는다.
- `→ (*… → Boolean)`: 첫 번째 또는 두 번째 술어 함수 중 하나를 호출하는 함수를 반환한다.
- 

## 예제

```js
const gt10 = x => x > 10;
const even = x => x % 2 === 0;
const f = R.either(gt10, even);
f(101); //=> true
f(8); //=> true
```
- `f(101)`: `gt10` 함수에 인자를 전달한 결과와 `even` 함수에 인자를 전달한 결과를 || 연산자로 묶은 함수 `f`에 101을 전달하면, `gt10`에 101이 먼저 전달되고 참이 반환된다. || 연산자로 연결되어 있기 때문에 `even`을 실행하지 않고도 `f(101)`는 true를 반환한다.
- `f(8)`: `gt10` 함수에 인자를 전달한 결과와 `even` 함수에 인자를 전달한 결과를 || 연산자로 묶은 함수 `f`에 8을 전달하면, `gt10`에 8이 먼저 전달되고 거짓이 반환된다. || 연산자로 연결되어 있기 때문에 첫 번째가 거짓이므로 두 번째가 참인자 확인하기 위해 `even` 함수에 8을 전달한다. 이 때 true가 반환되므로 `f(8)`의 결과는 true이다.


```js
R.either(Maybe.Just(false), Maybe.Just(55)); // => Maybe.Just(55)
R.either([false, false, 'a'], [11]) // => [11, 11, "a"]
```

## References
- https://ramdajs.com/docs/#either
- https://github.com/ramda/ramda/blob/master/test/either.js
- https://github.com/ramda/types/blob/develop/types/either.d.ts
