## unary
> Wraps a function of any arity (including nullary) in a function that accepts exactly 1 parameter.
- 임의의 (인자를 받지 않는 경우를 포함하여) 인자 수를 갖는 함수를 1개의 매개변수만 허용하는 함수로 레핑(Wraps)한다.
> Any extraneous parameters will not be passed to the supplied function.
- 주어진 함수에 외부 매개변수는 전달되지 않는다.
> See also binary, nAry.

### 설명

### 표현
```
(a → b → c → … → z) → (a → z)
```

### 예제
```js
const takesTwoArgs = function(a, b) {
  return [a, b];
};
takesTwoArgs.length; //=> 2
takesTwoArgs(1, 2); //=> [1, 2]

const takesOneArg = R.unary(takesTwoArgs);
takesOneArg.length; //=> 1
// Only 1 argument is passed to the wrapped function
takesOneArg(1, 2); //=> [1, undefined]
```
- `takesTwoArgs`는 인자를 두 개 받아서 이를 하나의 값으로 만들기 위해 순서가 정해진 나열 형태인 배열이란 자료 구조를 사용하는 다수의 인자를 하나의 인자로 만들어 주는 함수이다.
- [`function.length`의 표현식](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/length)은 함수가 받는 인자의 수를 추측한 값이다. `takesTwoArgs` 함수는 2개의 인자를 받으므로 legnth 값이 2이다.
- `takesOneArg(1, 2)`는 값을 두 개 받아서 하나의 값으로 만든다.
- `const takesOneArg = R.unary(takesTwoArgs)`: `R.unary` 함수를 통해서 2개의 값을 하나로 만드는 함수 `takesTwoArgs`를 받아서, 하나의 인자를 받는 함수로 바꾼다.
- `takesOneArg.length`의 값이 1인 것을 통해서 `takesOneArg` 함수는 하나의 인자를 받는 것을 확인할 수 있다.

## References
- https://ramdajs.com/docs/#unary
