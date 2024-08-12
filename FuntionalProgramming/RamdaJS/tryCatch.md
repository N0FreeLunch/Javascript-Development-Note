## tryCatch
> tryCatch takes two functions, a tryer and a catcher.
- tryCatch는 2개의 함수, tryer과 catcher를 받는다. 

> The returned function evaluates the tryer; if it does not throw, it simply returns the result.
- 함수의 반환값은 tryer (함수를) 평가하고, (tryer 함수가 실행되는 중에) (값을 던지는) throw가 발생하지 않는다면, (tryer의 평가) 결과 값을 반환한다.

> If the tryer does throw, the returned function evaluates the catcher function and returns its result.
- 만약 tryer이 (tryer이 함수의 실행 과정에서) (값을) 던진다면, 반환된 함수는 catcher 함수를 평가하고 그 결과 값을 반환한다.

> Note that for effective composition with this function, both the tryer and catcher functions must return the same type of results.

### 설명

### 표현
```
(…x → a) → ((e, …x) → a) → (…x → a)
```

### 예제
```js
R.tryCatch(R.prop('x'), R.F)({x: true}); //=> true
R.tryCatch(() => { throw 'foo'}, R.always('caught'))('bar') // =>
'caught'
R.tryCatch(R.times(R.identity), R.always([]))('s') // => []
R.tryCatch(() => { throw 'this is not a valid value'}, (err, value)=>({error : err,  value }))('bar') // => {'error': 'this is not a valid value', 'value': 'bar'}
```
- `R.tryCatch(R.prop('x'), R.F)({x: true})`: trier에 해당하는 `R.prop('x')`에는 값을 던지는 어떠한 구문도 포함되어 있지 않다. 따라서 항상 trier만 실행되고 catcher에 해당하는 함수는 실행되지 않으므로 trier의 평가 결과인 `R.prop('x')`가 실행된 결과인 오브젝트 하나를 받아서 프로퍼티 x의 값을 반환하는 함수가 반환된다. 이 함수는 `R.tryCatch(R.prop('x'), R.F)`의 결과이며 이 함수를 fn이라고 했을 때 `fn({x: true})`으로 오브젝트를 인자로 받아 그 결과값을 반환하게 된다.
- `R.tryCatch(() => { throw 'foo'}, R.always('caught'))('bar')`: trier에 해당하는 `() => { throw 'foo'}`는 반드시 값을 던지는 함수이다. 이로 인해 trier의 실행 도중에 throw 구문이 실행이 되며, catcher 함수가 실행된다. catcher 함수인 `R.always('caught')`가 실행되어 반환된다. `R.tryCatch(() => { throw 'foo'}, R.always('caught'))`의 실행 결과는 `R.always('caught')`의 반환값을 반환하게 되며 어떠한 인자든 하나 받아서 무조건 `'caught'`라는 값을 반환한다. `R.tryCatch(() => { throw 'foo'}, R.always('caught'))`를 fn이라고 했을 때 `fn('bar')`가 최종적으로 실행되며, 이 때 fn은 항상 `'caught'`를 반환하므로 최종 반환 값은 `'caught'`가 된다.
- `R.tryCatch(R.times(R.identity), R.always([]))('s')`: trier에 해당하는 `R.times(R.identity)`는 throw 구문이 없으므로 catcher은 실행되지 않고 trier만 실행된다. 반환 값은 주어진 값 n에 대해 0부터 n-1까지의 값을 `R.identity`에 전달한 결과를 나열한 배열이다. 이 함수를 fn이라고 할 때 `fn('s')`를 실행하는데, `s`는 횟수가 아니므로 유효한 값이 될 수 없다. 이 때 times 함수는 빈 배열을 반환하므로 결과값은 `[]`가 된다.
- `R.tryCatch(() => { throw 'this is not a valid value'}, (err, value)=>({error : err,  value }))('bar')`: trier에 해당하는 `() => { throw 'this is not a valid value'}` 구문은 반드시 값을 던지도록 되어 있다. 따라서 catcher가 실행되는데 catcher은 `(err, value)=>({error : err,  value })`을 실행하며, 이 때 반환 값은 `{error : err,  value }`라는 오브젝트이다. 이때 catcher의 첫 번째 인자는 trier에서 던져진 값을 받으며, 두 번째 인자는 자동으로 커링된다. 커링이 되었기 때문에 반환 결과는 `value` 인자를 받아서 catcher 함수를 최종 평가한 결과를 반환한다. catcher가 평가된 반환 값으로 err 값은 머금은 채 커링된 형태를 함수 fn이라고 했을 때, `fn('bar')`의 결과는 `{'error': 'this is not a valid value', 'value': 'bar'}`가 된다. (참고로 `{a: b, c}`의 꼴의 리터럴 오브젝트는 b=1, c=2의 값을 얻어서 `{a: 1, b: 2}`의 꼴이된다.)

## Referneces
- https://ramdajs.com/docs/#tryCatch
