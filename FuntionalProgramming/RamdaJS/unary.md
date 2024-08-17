## unary
> Wraps a function of any arity (including nullary) in a function that accepts exactly 1 parameter.
- 임의의 (인자를 받지 않는 경우를 포함하여) 인자 수를 갖는 함수를 1개의 매개변수만 허용하는 함수로 레핑(Wraps)한다.
> Any extraneous parameters will not be passed to the supplied function.
- (허용된 하나의 파라메터 이외의) 나머지 파라메터는 함수에 공급되지 않는다.
> See also binary, nAry.

### 설명
- 임의의 인자를 받을 수 있는 함수를 하나의 인자를 받는 함수로 바꾼다. `R.unary`에 의해 반환된 함수는 원본 함수와 거의 동일한 기능을 갖지만 인자를 하나만 받을 수 있다. 첫 번째 인자만을 함수 내부로 전달하고, 두 번째 인자 부터는 함수 내부로 전달하지 않는다.

### 표현
```
(a → b → c → … → z) → (a → z)
```
- `(a → b → c → … → z) →`: 첫 번째 인자로 임의의 인자 갯수를 받을 수 있는 함수를 받는데, `a → b → c → … →`까지가 임의의 인자를 받고, `→ z`라는 반환 값을 갖는 함수라는 의미이다.
- `→ (a → z)`: 함수를 반환하는데, 첫 번째 인자로 받는 함수의 첫 번째 인자 `a`와 동일한 타입 파라메터를 갖는다는 것을 알 수 있다. 이는 첫 번째 함수의 첫 번째 인자만을 받는 함수가 반환되기 때문이다.

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
- `takesTwoArgs`는 인자를 두 개 받아서 이를 하나의 값으로 만들기 위해 순서가 정해진 나열 형태인 배열이란 자료 구조를 사용하여 다수의 값을 하나의 값으로 만들어 주는 함수이다.
- [`function.length`의 표현식](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/length)은 함수가 받는 인자의 수를 추측한 값이다. `takesTwoArgs` 함수는 2개의 인자를 받으므로 legnth 값이 2이다.
- `takesOneArg(1, 2)`는 값을 두 개 받아서 하나의 값으로 만든다.
- `const takesOneArg = R.unary(takesTwoArgs)`: `R.unary`는 단항 함수를 만드는 것으로 두 번째 인자 부터는 무효화한다.
- `takesOneArg.length`의 값이 1인 것을 통해서 `takesOneArg` 함수는 하나의 인자를 받는 것을 확인할 수 있다.
- `takesOneArg(1, 2)`: 두 인자 중에서 하나의 인자만 전달되고, 나머지 인자는 무효화 되어 전달되지 않으므로 결과 값은 `[1, undefined]`이 된다.

## References
- https://ramdajs.com/docs/#unary
