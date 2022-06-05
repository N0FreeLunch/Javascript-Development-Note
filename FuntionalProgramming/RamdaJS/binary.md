## binary
- R.binary()
> Wraps a function of any arity (including nullary) 
- (널을 받는 인수를 포함한) 임의의 인수를 가지는 어떤 함수를 감싼 새로운 함수를 만든다.
> in a function that accepts exactly 2 parameters. 
- 새 함수는 해당 함수에서 딱 두 개의 파라메터만을 함수 내부로 전달한다.
> Any extraneous parameters will not be passed to the supplied function.
> 전달되는 두 개의 함수 이외의 나머지 파라메터는 함수 내부로 전달 되지 못한다.

## 표현
```
(a → b → c → … → z) → ((a, b) → z)
```
- `(a → b → c → … → z)`는 인자로 `a` `b` `c` ... `y` 를 받는 함수가 있다고 하자. 임의의 수의 인자를 받는 함수이다.
- `(a → b → c → … → z)`를 `R.binary()` 함수 안에 넣으면 인자가 2개만 받는 함수가 된다.
- 따라서 `((a, b) → z)`가 되는 것.

## 설명
- 여러 인자를 가지는 임의의 함수를 `R.binary()` 함수에 넣으면 인자를 딱 2개만 받는 함수로 변환한 함수를 반환한다.
- 인자의 갯수를 여럿 가지면서 인자마다 각각의 독특한 기능을 하는 것이 아니라 인자의 갯수가 많아도 적어도 동일한 방식의 연산을 하는 함수의 경우에 인자의 갯수를 두 개만 지정할 때 사용한다.

## 예제
```
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
- [function.length](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/length) 표현은 함수가 요구하는 인자의 개수를 의미한다. 따라서 `takesThreeArgs.length;` 값은 3이 된다.
- `R.binary(takesThreeArgs)` `R.binary` 함수에 `takesThreeArgs`란 함수를 인자로 넣었다. 이렇게 생성된 함수 `takesTwoArgs`의 인자의 갯수를 확인하니 (`takesTwoArgs.length`) `2`라는 값이 나왔다.
- `takesTwoArgs(1, 2, 3);`를 하니 `[1, 2, undefined]`라는 결과 값이 나온 것을 보고 나머지 인자 하나를 못 받는 함수가 되었다는 것을 알 수 있다.
- 곧, `takesThreeArgs`라는 함수가 3개의 인자를 받았지만 `R.binary` 함수에 넣자 인자를 두 개 밖에 못 받는 `takesTwoArgs`함수가 되었다.
- 인자를 두 개만 받을 수 있지만 기능은 동일하기 때문에 내부 로직에서는 세 번째 인자를 받지 못하여 `[1, 2, undefined]`라는 결과 값이 나왔다.

## Reference
- https://ramdajs.com/docs/#binary
