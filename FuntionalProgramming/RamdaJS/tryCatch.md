## tryCatch
> tryCatch takes two functions, a tryer and a catcher.
- tryCatch는 2개의 함수, tryer과 catcher를 받는다. 

> The returned function evaluates the tryer; if it does not throw, it simply returns the result.
- 함수의 반환값은 tryer (함수를) 평가하고, (tryer 함수가 실행되는 중에) (값을 던지는) throw가 발생하지 않는다면, (tryer의 평가) 결과 값을 반환한다.

> If the tryer does throw, the returned function evaluates the catcher function and returns its result.
- 만약 tryer이 (tryer이 함수의 실행 과정에서) (값을) 던진다면, 반환된 함수는 catcher 함수를 평가하고 그 결과 값을 반환한다.

> Note that for effective composition with this function, both the tryer and catcher functions must return the same type of results.
- tryCatch 함수로 효과적인 함수의 조합을 하기 위해서는 tryer 함수와 catcher 함수 모두 동일한 결과 타입을 반환해야 한다.

### 설명
- tryCatch 함수는 tryer과 catcher 함수를 하나씩 받으며 tryCatch의 최종 반환 값은 함수로 반환 함수를 `returnedFn`이라고 할 때 `returnedFn()`의 형태로 실행이 된다. `returnedFn()`로 함수가 실행되면 tryer 함수를 실행하고 tryer 함수에서 무언가 throw 되면 catcher 함수를 실행한다. 이 때 `returnedFn(...args)`로 인자를 받을 경우에는, tryer 함수를 실행할 때 인자 `...arg`를 전달하며, tryer 실행 도중에 throw 되어 catcher 함수를 실행하게 되면 catcher 함수의 첫 번째 인자로는 throw로 던져진 값이 전달되고, 두 번째 인자부터는 `...arg` 값을 전달 받아 실행이 된다.

### 표현
```
(…x → a) → ((e, …x) → a) → (…x → a)
```
- `(…x → a) →`: 첫 번재 인자로 tryer을 받는다. `…x`는 임의의 갯수의 인자를 받는다는 의미이다. tryCatch의 최종 반환된 함수가 실행될 때 받는 인자와 동일하다. 최종 반환 함수가 실행될 때 함께 받는 인자가 tryer 함수의 인자로 전달되며 실행된다. tryer 함수가 무언가를 throw 한다면 catcher이 실행된다. tryer 함수의 반환값은 catcher 함수의 반환 값과 동일한 타입으로 하는 것이 좋은데 tryCatch의 최종 반환 함수의 실행 결과에 따른 분기 처리를 최소화하기 위함이다.
- `→ ((e, …x) → a) →`: 두 번째 인자로 catcher을 받는다. tryCatch의 최종 반환된 함수가 실행될 때 tryer 함수를 실행하면서 무언가를 throw 했을 때 실행되는 함수이다. 첫 번째 인자로 에러에 해당하는 `e`를 받는데, 꼭 에러 타입이 아니라도 throw에 의해 던져진 대상을 받는다. 그리고 `…x`로 알 수 있듯이 나머지 인자로는 tryCatch의 최종 반환된 함수가 실행될 때 함께 받은 인자를 전달 받아 실행된다.
- `→ (…x → a)`: 최종적으로 반환된 값은 함수인데, `…x`를 인자로 받아서 평가되는 함수이다. `…x`는 tryer 함수가 실행될 때 인자로 전달되며, catcher 함수가 실행된다면 마찬가지로 인자로 전달한다.

### 예제
```js
R.tryCatch(R.prop('x'), R.F)({x: true}); //=> true
R.tryCatch(() => { throw 'foo'}, R.always('caught'))('bar') // =>
'caught'
R.tryCatch(R.times(R.identity), R.always([]))('s') // => []
R.tryCatch(() => { throw 'this is not a valid value'}, (err, value)=>({error : err,  value }))('bar') // => {'error': 'this is not a valid value', 'value': 'bar'}
```
- `R.tryCatch(R.prop('x'), R.F)({x: true})`: `R.tryCatch(R.prop('x'), R.F)`로 반환된 함수는 `{x: true}`라는 인자 값을 받아 실행이 된다. tryer에 해당하는 `R.prop('x')`에는 값을 던지는 어떠한 구문도 포함되어 있지 않다. 따라서 항상 tryer만 실행되고 catcher에 해당하는 함수는 실행되지 않는다. tryer 함수가 실행될 때는 `{x: true}`을 인자로 전달한다. 곧, `R.prop('x')({x: true})`가 실행되어 `true`란 값을 얻는다.
- `R.tryCatch(() => { throw 'foo'}, R.always('caught'))('bar')`: `R.tryCatch(() => { throw 'foo'}, R.always('caught'))`로 반환된 함수는 `'bar'`라는 인자를 받아 실행된다. tryer이 실행될 때 `'bar'` 인자가 전달이 되지만 tryer 함수에 파라메터가 정의되어 있지 않으므로 인자가 전달되지는 않는 형태 `() => { throw 'foo'}`이다. tryer의 실행에 의해 throw 구문이 동작하며 이에 따라 catcher 함수가 실행된다. catcher 함수인 `R.always('caught')`는 던져진 값을 첫 번째 인자로, 나머지 인자로 `'bar'`를 전달 받아 `R.always('caught')('foo', 'bar')`가 된다. `R.always('caught')` 함수는 어떠한 인자든 하나 받아서 무조건 `'caught'`라는 값을 반환한다. 따라서 최종 결과 값은 `'caught'`가 된다.
- `R.tryCatch(R.times(R.identity), R.always([]))('s')`: `R.tryCatch(R.times(R.identity), R.always([]))`로 반환된 함수는 `'s'`라는 인자를 받아 실행된다. tryer에 해당하는 `R.times(R.identity)`는 throw 구문이 없으므로 catcher은 실행되지 않고 tryer만 실행된다. 반환 값은 주어진 값 n에 대해 0부터 n-1까지의 값을 `R.identity`에 전달한 결과를 나열한 배열이다. 그런데 tryer로 전달된 인자인 `'s'`는 횟수가 아니므로 유효한 값이 될 수 없다. 이 때 times 함수는 빈 배열을 반환하므로 결과값은 `[]`가 된다.
- `R.tryCatch(() => { throw 'this is not a valid value'}, (err, value)=>({error : err,  value }))('bar')`: `R.tryCatch(() => { throw 'this is not a valid value'}, (err, value)=>({error : err,  value }))`로 반환된 함수는 인자 `'bar'`를 전달 받아 실행된다. tryer인 `() => { throw 'this is not a valid value'}`는 파라메터가 없으므로 `'bar'`를 전달 받지 않으며, 내부 코드는 반드시 값을 던지도록 되어 있다. 따라서 catcher가 실행되는데 catcher은 `(err, value)=>({error : err,  value })`을 실행하며, `err` 파라메터로 `'this is not a valid value'`를 전달하고, `value` 파라메터에는 `'bar'`를 전달한다. 평가로 얻은 최종 결과는 `{'error': 'this is not a valid value', 'value': 'bar'}`가 된다. (참고로 `{a: b, c}`의 꼴의 리터럴 오브젝트는 b=1, c=2의 값을 얻어서 `{a: 1, b: 2}`의 꼴이된다.)

## Referneces
- https://ramdajs.com/docs/#tryCatch
