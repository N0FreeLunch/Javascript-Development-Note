## both

> A function which calls the two provided functions and returns the && of the results.
- 두 개의 함수를 받아 호출하여 결과값을 &&로 비교한 값을 반환한다.

> It returns the result of the first function if it is false-y and the result of the second function otherwise.
- 만약 첫 번째 함수가 false-y이면 첫 번째 함수를 반환하고, 그렇지 않으면 두 번째 함수를 반환한다.

> Note that this is short-circuited, meaning that the second function will not be invoked if the first returns a false-y value.
- 짧게 동작할 수 있는데(short-circuited), 첫 번째가 false-y 값을 반환하면 두 번째 함수는 호출되지 않는다는 의미이다.

> In addition to functions, R.both also accepts any fantasy-land compatible applicative functor.
- 추가로, R.both는 어떠한 fantasy-land 사양의 applicative functor과도 호환될 수 있다.

> See also [either](./either.md), [allPass](./allPass.md), [and](./and.md).

### 설명
- `R.both` 함수는 두 개의 술어함수(또는 반환값이 참 거짓을 판단할 수 있는 truely or falsy)를 받아 함수를 하나 반환한다. 반환된 함수는 인자를 받는데, 반환되기 이전에 받은 첫 번째 함수에 인자를 전달하여 얻은 결과 값이 truely이면, 두 번째 함수에 인자를 전달하여 반환된 값을 반환하며, 첫 번째 함수에 인자를 전달한 값이 falsy이면 첫 번째 인자의 반환값을 반환한다. 이 때, 두 번째 함수에는 인자를 전달하지 않는다.
- 람다의 `R.and` 프로그래밍 언어의 `&&` 처럼 앞의 값이 참이면 앞의 값이 최종 값이며, 앞의 값이 거짓이면 뒤의 값이 최종값이 되는 연산을 한다. 논리학의 논리 연산과 프로그래밍의 논리 연산자의 동작은 차이가 있으니 주의하자.
- 최종 반환된 값은 불리언 타입이 아닐 수 있다. 단순히 참, 거짓을 체크하는 것이 아닌 반환된 값을 이용한다면 위의 동작 방식에 주의해야 하지만, 반환값의 참, 거짓만 확인하고자 한다면 다음과 같이 간단한 이해를 할 수 있다. 두 개의 술어함수를 받고 함수가 반환되는데, 반환된 함수는 하나의 인자 받아 미리 받은 두 개의 술어함수에 인자로 할당했을 때 둘 중 하나라도 거짓이라면 거짓을 둘 다 참이라면 참은 반환하는 함수이다.

### 문법
```
R.both(f, g): function
```
- `f`: A predicate
- `g`: Another predicate
- Returns function a function that applies its arguments to `f` and `g` and `&&`s their outputs together.

### 표현
```
(*… → Boolean) → (*… → Boolean) → (*… → Boolean)
```
- `(*… → Boolean) → `: 술어 함수를 하나 받는다. 이를 f라 하자.
- `→ (*… → Boolean) →`: 술어 함수를 또 하나 받는다. 이를 g라 하자.
- `→ (*… → Boolean)`: 함수를 반환하는데, 이 함수는 `*…`를 인자로 받아 `f(*…) && g(*…)`의 동작을 수행한다. 이때, 인자로 받은 값은 술어 함수 각각에 전달하는 값으로 동일한 종류와 갯수의 인자를 받아야 한다.

### 예제
```js
const gt10 = R.gt(R.__, 10)
const lt20 = R.lt(R.__, 20)
const f = R.both(gt10, lt20);
f(15); //=> true
f(30); //=> false

R.both(Maybe.Just(false), Maybe.Just(55)); // => Maybe.Just(false)
R.both([false, false, 'a'], [11]); //=> [false, false, 11]
```
- `R.__`는 미리 받아야 할 인자를 나중에 받을 수 있도록 한다. `gt10`함수는 `R.gt(R.__, 10)`에서 `R.__` 부분에 해당하는 인자를 받게 된다. 곧, `gt10` 함수는 받은 인자가 10보다 큰지 체크하여 참, 거짓을 반환하는 함수이다.
- `R.lt(R.__, 20)`으로 만들어진 `lt20`함수는 인자로 `R.__` 부분에 해당하는 인자 값을 받는다. 곧, 받은 인자가 20보다 작은지를 체크하여 참, 거짓을 반환하는 함수이다.
- `R.both`는 인자롤 받은 두 술어함수에 동일한 인자를 넣어 두 술어함수를 만족하면 참, 하나라도 거짓이거나 모두 거짓인 경우 거짓을 반환하는 함수가 된다.
- `R.both(gt10, lt20)`으로 만들어진 f는 10보다 크고 20보다 작은지를 체크하는 술어함수가 된다.
- `f(15);`에서 15는 10보다 크고 20보다 작으므로 참을 반환한다.
- `f(30);`애서 30은 10보타 크다는 것은 참이지만 20보다 크다는 것은 거짓이므로 거짓을 반환한다.

## References
- https://ramdajs.com/docs/#both
- https://github.com/ramda/ramda/blob/master/test/bind.js
- https://github.com/ramda/types/blob/develop/types/bind.d.ts
