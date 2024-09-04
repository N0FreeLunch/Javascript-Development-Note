## useWith
> Accepts a function fn and a list of transformer functions and returns a new curried function.
- 함수 fn과 변형 함수를 받아 커링된 함수를 반환한다.
> When the new function is invoked, it calls the function fn with parameters consisting of the result of calling each supplied handler on successive arguments to the new function.
- 새로운 함수가 호출될 때, 새로운 함수에 전달된 연속된 인자에 대해 제공된 헨들러 각각을 호출한 결과로 구성된 파라메터와 함께 함수 fn을 호출한다.

> If more arguments are passed to the returned function than transformer functions, those arguments are passed directly to fn as additional parameters.
- 반환된 함수에 변형 함수들 보다 더 많은 인자가 전달된다면 이들 인자는 fn에 추가 파라메터로 직접적으로 전달된다.
> If you expect additional arguments that don't need to be transformed, although you can ignore them, it's best to pass an identity function so that the new function reports the correct arity.
- 추가된 파라메터들이 변형되지 않기를 원한다면 항등함수를 전달하는 것으로 무시할 수 있다. 항등함수를 사용하는 것으로 (반환된) 새 함수는 올바른 인자의 수를 알려준다.

> See also converge.

### 설명
- 어떤 함수에 인자를 전달할 때 인자를 그냥 전달하지 않고 지정한 함수에 의해 변경된 값을 인자로 전달하는 기능을 레핑한 새로운 함수를 생성한다.
- 인자의 값을 변경하는 함수를 변형함수라고 하며, 변형함수는 두 번째 인자에 배열의 원소로 전달한다. 이 배열의 첫 번째 변형함수는 첫 번째 인자를 변경하고, 두 번째 번형함수는 두 번째 인자를 변경하는 식으로 대응된다. 배열에 나열된 변형함수의 갯수는 몇 개의 인자를 전달해야 하는지 알 수 있는 힌트를 제공한다.
- 만약 전달된 인자의 갯수보다 변형함수를 나열한 배열이 적은 경우 나중에 전달되거나 나열된 인자는 대응되는 변형함수가 없고, 매칭되는 변형함수가 없는 경우 원본 함수(fn)에 인자를 그대로 전달한다.

### 표현
```
((x1, x2, …) → z) → [(a → x1), (b → x2), …] → (a → b → … → z)
```
- `((x1, x2, …) → z) → `: 첫 번째 인자로 실행하고자하는 함수를 받는다.
- `→ [(a → x1), (b → x2), …] →`: 두 번째 인자로 변형함수를 나열한 배열을 받는다. 이때 변형함수의 타입 파라메터는 최종 반환 함수가 받는 인자의 타입 a,b,c...을 파라메터로 하고 첫 번째 인자로 받은 함수가 받는 파라메터 x1, x2, x3...을 반환값으로 하는 인자를 받아 첫 번째 인자로 받은 함수에 전달하기 위한 인자로 변경하기 위한 역할을 한다는 것을 나타낸다.
- `→ (a → b → … → z)`: 인자를 받아서 변환된 인자를 첫 번째 인자로 받은 함수에 전달해서 반환된 결과값을 최종 반환 값으로 하는 함수를 반환한다.

### 예제
```js
R.useWith(Math.pow, [R.identity, R.identity])(3, 4); //=> 81
R.useWith(Math.pow, [R.identity, R.identity])(3)(4); //=> 81
R.useWith(Math.pow, [R.dec, R.inc])(3, 4); //=> 32
R.useWith(Math.pow, [R.dec, R.inc])(3)(4); //=> 32
```
- `R.useWith(Math.pow, [R.identity, R.identity])(3, 4)`는 `[R.identity, R.identity]`를 통해서 인자를 두 개 받아야 한다는 것을 알려준다. 항등함수이므로 인자 `(3, 4)`가 전달될 때 3과 4는 `Math.pow` 함수에 그대로 전달된다. 반환된 함수는 커링이 되므로 `R.useWith(Math.pow, [R.identity, R.identity])(3)(4)`도 마찬가지로 동작한다.
- `R.useWith(Math.pow, [R.dec, R.inc])(3, 4)`는 `[R.dec, R.inc]`를 통해서 인자를 두 개 받아야 한다는 것을 알려준다. 반환된 함수에 전달된 인자 `(3, 4)`는 각각 변형함수 `R.dec`과 `R.inc`에 전달이 되고, `R.dec(3)`는 2이고  `R.inc(4)`는 5이므로 `Math.pow`에는 2와 5의 인자가 전달된다. 2^5이므로 32의 값을 갖는다.

## References
- https://ramdajs.com/docs/#useWith
