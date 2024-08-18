## uncurryN
> Returns a function of arity n from a (manually) curried function.
- (수동으로) 커링된 함수로 부터 n의 인자 수를 가진 함수를 반환한다.

> Note that, the returned function is actually a ramda style curryied function, which can accept one or more arguments in each function calling.
- 반환된 함수는 실제로 ramda 스타일의 커링된 함수라는 것에 주목하라. 커링된 함수는 각각의 함수의 호출에서 하나 또는 더 많은 인자를 받을 수 있다.

> See also curry, curryN.

### 설명

### 표현
```
Number → (a → b → c … → z) → ((a → b → c …) → z)
```
- `Number →`:
- `→ (a → b → c … → z) →`: 두 번째 인자로 함수를 받는데, 이 함수는 커링된 함수이다. `a → b → c … →`로 임의의 인자를 받고, 반환값 `→ z`를 갖는 함수이다.
- `→ ((a → b → c …) → z)`: 

### 예제
```js
const addFour = a => b => c => d => a + b + c + d;

const uncurriedAddFour = R.uncurryN(4, addFour);
uncurriedAddFour(1, 2, 3, 4); //=> 10
```

## Referneces
- https://ramdajs.com/docs/#uncurryN
