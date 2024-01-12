## nAry
> Wraps a function of any arity (including nullary) in a function that accepts exactly n parameters. Any extraneous parameters will not be passed to the supplied function.
- 임의의 인자의 갯수(인자가 하나도 없는 것을 포함하여)를 갖는 어떤 함수를 씌운다(wraps). `nAry` 함수로 감싸진 함수는 정확히 n개의 파라메터를 받으며, 지정한 n개 이외의 여분의 인자는 주어진(원본) 함수에 파라메터를 전달하지 않는다.

> See also binary, unary.

### 설명
- 함수와 수를 받아서 함수의 파라메터 중에서 지정한 수 만큼의 파라메터만 적용시킨 결과 함수를 얻는다.
- 첫 번째 인자로 적용시킬 파라메터의 수를 정한다. 두 번째 인자로 함수를 전달한다.
- 반환된 함수는 인자를 몇 개 받든 반환 되기 전 첫 번째 인자에서 지정한 갯수의 인자만을 받은 결과를 갖는다.

### 표현
```
Number → (* → a) → (* → a)
```
- `Number → ` 첫 번째 인자로는 인자의 갯수를 받는다.
- `→ (* → a) →` 두 번째 인자로는 임의의 타입과 수를 갖는 인자를 받는 함수를 받는다.
- `→ (* → a)` 두 번째 인자의 함수가 반환하는 결과 타입의 결과를 반환한다. 이는 인자를 몇개를 받든 두 번째 인자로 받은 함수의 반환값과 최종 결과 같의 타입이 동일하다는 것을 의미한다.

### 예제
```js
const takesTwoArgs = (a, b) => [a, b];

takesTwoArgs.length; //=> 2
takesTwoArgs(1, 2); //=> [1, 2]

const takesOneArg = R.nAry(1, takesTwoArgs);
takesOneArg.length; //=> 1
// Only `n` arguments are passed to the wrapped function
takesOneArg(1, 2); //=> [1, undefined]
```
- `takesTwoArgs` 함수는 인자를 두 개 받아서 받은 순서대로 인자를 원소로 나열한 배열을 반환한다.
- `R.nAry(1, takesTwoArgs)`는 `takesTwoArgs` 1개의 인자를 적용한 결과값을 얻는다는 것인데, 원래 인자를 2개 받으면 `[1, 2]`가 나와야 하지만, 하나의 인자만 적용되어 `[1, undefined]`의 결과가 된다.

## Reference
- https://ramdajs.com/docs/#nAry
