## tryCatch
> tryCatch takes two functions, a tryer and a catcher.
- tryCatch는 2개의 함수, tryer과 catcher를 받는다. 

> The returned function evaluates the tryer; if it does not throw, it simply returns the result.
- 함수의 반환값은 tryer (함수를) 평가하고, (tryer 함수가 실행되는 중에) (값을 던지는) throw가 발생하지 않는다면, (tryer의 평가) 결과 값을 반환한다.

> If the tryer does throw, the returned function evaluates the catcher function and returns its result.
- 만약 tryer이 (tryer이 함수의 실행 과정에서) (값을) 던진다면,

> Note that for effective composition with this function, both the tryer and catcher functions must return the same type of results.

### 설명
- 

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
- `R.tryCatch(R.prop('x'), R.F)({x: true})`: trier에 해당하는 `R.prop('x')`에는 값을 던지는 어떠한 구문도 포함되어 있지 않다. 따라서 항상 trier만 실행되고 catcher에 해당하는 함수는 실행되지 않으므로 trier의 평가 결과인 true만을 반환한다.

## Referneces
- https://ramdajs.com/docs/#tryCatch
