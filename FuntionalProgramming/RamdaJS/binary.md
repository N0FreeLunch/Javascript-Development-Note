## binary
> Wraps a function of any arity (including nullary) 
- 임의의 인자를 가지는 함수(인자를 받지 않는 (nullary) 함수를 포함하여)를 레핑한다.
> in a function that accepts exactly 2 parameters. 
- 새 함수는 해당 함수에서 딱 두 개의 파라메터만을 함수 내부로 전달한다.
> Any extraneous parameters will not be passed to the supplied function.
> 전달되는 두 개의 함수 이외의 나머지 파라메터는 (레핑 대상 함수의 인자로) 전달 되지 못한다.

### 설명
- 임의의 인자의 갯수를 가지는 임의의 함수를 `R.binary()` 함수에 넣으면 인자를 딱 2개만 받는 함수로 변환된 함수를 반환한다.
- 인자의 갯수만 2개로 달리 받으면서 동일한 기능을 해야 하는 함수이기 때문에 반환값을 만들어 낼 때 인자의 유무에 따라 함수의 동작이 완전히 달라지지 않도록 만들어진 함수에 적용하는 것이 좋다. 주어지는 인자의 갯수에 따라 함수의 반환되는 종류가 전혀 호환이 되지 않는다든가 하는 경우의 함수에는 적용하지 않는 편이 좋다.

### 문법
```
R.binary(fn): function
```
> `fn`: The function to wrap.
- `fn`: 레핑한 함수
> Returns function A new function wrapping `fn`. The new function is guaranteed to be of arity 2.
- `fn`을 레핑한 새로운 함수를 반환한다. 

### 표현
```
(a → b → c → … → z) → ((a, b) → z)
```
- `(a → b → c → … → z)`: 인자로 `a` `b` `c` ... `y` 를 받는 함수가 있다고 하자. 임의의 수의 인자를 받는 함수이다. `(a → b → c → … → z)`를 `R.binary()` 함수 안에 넣으면 인자가 2개만 받는 함수가 된다.
- `((a, b) → z)`: 반환된 함수는 인자를 `a` `b` `c` ... `y`로 임의의 갯수를 받던 함수에서 `(a, b)` 두 개만을 받는 함수로 변환된다. 첫 번째 인자로 받은 함수와 동일한 함수이므로 반환 타입의 종류는 동일하게 `z`가 된다.

### 예제
```js
const takesThreeArgs = function(a, b, c) {
  return [a, b, c];
};
takesThreeArgs.length; //=> 3
takesThreeArgs(1, 2, 3); //=> [1, 2, 3]

const takesTwoArgs = R.binary(takesThreeArgs);
takesTwoArgs.length; //=> 2
// Only 2 arguments are passed to the wrapped function
takesTwoArgs(1, 2, 3); //=> [1, 2, undefined]
```
- [function.length](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/length) 표현은 함수가 요구하는 인자의 갯수를 의미한다. 따라서 `takesThreeArgs.length;` 값은 3이 된다.
- `R.binary(takesThreeArgs)` `R.binary` 함수에 `takesThreeArgs`란 함수를 인자로 넣었다. 이렇게 생성된 함수 `takesTwoArgs`의 인자의 갯수를 확인하니 (`takesTwoArgs.length`) `2`라는 값이 나왔다.
- `takesTwoArgs(1, 2, 3);`를 하니 `[1, 2, undefined]`라는 결과 값이 나온 것을 보고 나머지 인자 하나를 못 받는 함수가 되었다는 것을 알 수 있다.
- 곧, `takesThreeArgs`라는 함수가 3개의 인자를 받았지만 `R.binary` 함수에 넣자 인자를 두 개 밖에 못 받는 `takesTwoArgs`함수가 되었다.
- 인자를 두 개만 받을 수 있지만 기능은 동일하기 때문에 내부 로직에서는 세 번째 인자를 받지 못하여 `[1, 2, undefined]`라는 결과 값이 나왔다.

## References
- https://ramdajs.com/docs/#binary
- https://github.com/ramda/ramda/blob/master/test/binary.js
- https://github.com/ramda/types/blob/develop/types/binary.d.ts
