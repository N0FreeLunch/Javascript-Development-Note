## either

> A function wrapping calls to the two functions in an || operation, returning the result of the first function if it is truth-y and the result of the second function otherwise.
- 두 함수에 대한 호출(calls)을 || 연산으로 래핑하는 함수로, 참(에 상당하는 값)이면 첫 번째 함수의 결과를 반환하고 그렇지 않으면 (거짓에 상당하는 값이면) 두 번째 함수의 결과를 반환한다.
> Note that this is short-circuited, meaning that the second function will not be invoked if the first returns a truth-y value.
- 이것은 short-circuited(논리 연산을 수행할 때 왼쪽 피연산자만으로 전체 결과가 결정되면, 오른쪽 피연산자는 평가하지 않는 것)으로서, 두 번째 함수는 첫 번째 함수가 참(에 상당하는) 값을 반환하는 경우에, 두 번째 함수는 실행되지 않는다.
> In addition to functions, R.either also accepts any fantasy-land compatible applicative functor.
- 함수를 적용할 때, `R.either`는 어떠한 fantasy-land 호환으로 적용되는 펑터를 받을 수 있다.

> See also [both](./both.md), [anyPass](./anyPass.md), [or](./or.md).

## 설명

- 두 술어함수를 받아서 술어함수의 결과를 || 연산자로 연결한다. 술어 함수의 반환 값은 불리언이고, '첫 번째 술어 함수의 반환된 불리언 값' || '두 번째 술어함수의 반환된 불리언 값'으로 구성된다.
- 첫 번째 술어함수의 결과값이 참이라면, || 연산자에 의한 결과를 얻기 때문에 두 번째 술어함수를 평가하지 않아도 참을 반환하기 때문에 두 번째 술어함수를 실행하지 않는다.

## 문법

```
R.either(f, g): Fucntion 
```
> `f`: a predicate
- `f`: 어떤 술어함수
> `g`: another predicate
- `g`: 다른 술어 함수
> Returns function a function that applies its arguments to `f` and `g` and `||`s their outputs together.
- 함수를 반환한다. 이 함수는 (술어함수) `f`와 `g`에 함수의 인자를 전달하고, (각각의 함수의 결과에) OR 연산을 한다.

## 표현

```
(*… → Boolean) → (*… → Boolean) → (*… → Boolean)
```
- `(*… → Boolean) →`: 첫 번째 인자로 술어 함수를 받는다.
- `→ (*… → Boolean) →`: 두 번째 인자로 술어 함수를 받는다.
- `→ (*… → Boolean)`: 첫 번째 또는 두 번째 술어 함수의 결과를 OR 연산한다.
- 첫 번째 술어함수의 결과값이 참이라면, 첫 번째 술어 함수의 결과값을 반환하며 두 번째 술어함수는 평가하지 않는다.
- 첫 번째 술어함수의 결과가 거짓이고, 두 번째 술어함수의 술어함수의 결과값이 참이라면 두 번째 술어 함수의 결과값을 반환한다.
- 첫 번째 술어함수의 결과가 거짓이고, 두 번째 술어함수의 결과가 거짓이면 거짓을 반환한다.

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
```
- `Maybe.Just(false)`는 항상 false를 반환하는 함수이므로 `R.either`를 적용하면 첫 번째 술어 함수의 결과가 항상 거짓이므로 두 번째 술어함수가 반드시 평가되어야 하므로 `Maybe.Just(55)` 술어함수와 동일하다는 의미이다.

```js
R.either([false, false, 'a'], [11]) // => [11, 11, "a"]
```
- 위에서 적용된 인자는 술어함수가 아니며, fantasy-land 호환의 펑터를 받는 형태이다. 첫 번째 원소 `false`과 11을 OR 연산했을 때 11이 되며, 두 번째 원소 `false`과 11을 OR 연산했을 때 11이 되며, 세 번째 원소 `'a'`와 11을 비교 했을 때 `'a'`가 참이므로 `'a'`를 반환하며 11은 무시한다. 따라서 결과는 `[11, 11, "a"]`가 된다.

## References
- https://ramdajs.com/docs/#either
- https://github.com/ramda/ramda/blob/master/test/either.js
- https://github.com/ramda/types/blob/develop/types/either.d.ts
