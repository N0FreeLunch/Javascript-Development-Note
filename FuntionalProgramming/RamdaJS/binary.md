## binary
- R.binary()

## 표현
```
(a → b → c → … → z) → ((a, b) → z)
```

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
- `R.binary(takesThreeArgs)` `R.binary` 함수에 함수인 `takesThreeArgs`를 넣었다.

## Reference
- https://ramdajs.com/docs/#binary
