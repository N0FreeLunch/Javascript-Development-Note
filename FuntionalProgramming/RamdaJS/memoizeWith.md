## memoizeWith
> Creates a new function that, when invoked, caches the result of calling fn for a given argument set and returns the result. 
- 주어진 함수 fn에 대해 fn을 호출할 때 주어진 인자 세트와 반환한 결과를 캐싱하는 새로운 함수를 만든다.
> Subsequent calls to the memoized fn with the same argument set will not result in an additional call to fn; 
- 한 번 호출된 다음에는 fn의 저장된 값을 호출한다. 이 때 저장된 fn은 같은 인자가 지정되며 추가적인 호출의 결과를 가지지 않는다.
> instead, the cached result for that set of arguments will be returned.
- 대신, 지정된 인자에 대한 캐쉬된 결과를 반환한다.
> Care must be taken when implementing key generation to avoid key collision, or if tracking references, memory leaks and mutating arguments.

## 설명

## 표현
```
(*… → String) → (*… → a) → (*… → a)
```
- `(*… → String) →` 첫 번째 인자로 세팅된 `memoizeWith` 함수를 사용할 때 키로서 사용될 수 있도록 인자 세트를 문자열로 고정할 수 있는 함수를 받는다. 어떤 종류의 인자 세트를 받을 때 저장을 하고 동일한 종류의 인자 세트를 받을 경우 호출할 수 있도록 동일한 종류의 인자 세트인지 구분할 수 있는 키로서 사용되는 문자열을 반환할 수 있는 함수를 받는다.
- `→ (*… → a) →` 두 번째 인자로 첫 번째 인자로 받은 함수의 인자를 동일하게 받을 수 있는 함수를 받으며 이 함수는 한 번 호출되면 그 결과값을 저장하는 함수이다.
- `→ (*… → a)` 인자를 받아서 동일한 인자세트를 받아 첫 번째 인자로 받은 함수의 문자열 결과 값이 동일하다면 동일한 인자세트로 간주하고 동일한 인자세트를 받았을 때 저장된 결과 값을 반환하는 함수를 반환한다.

## 예제
```
let count = 0;
const factorial = R.memoizeWith(Number, n => {
  count += 1;
  return R.product(R.range(1, n + 1));
});
factorial(5); //=> 120
factorial(5); //=> 120
factorial(5); //=> 120
count; //=> 1
```
- `Number`는 주어진 인자를 수로 바꾸는 함수이다. 여기서는 수가 아닌 값은 `NaN`으로 반환하여 수치 연산에 잘못된 값이 있을 경우 알려 주는 역할을 한다.
- `R.memoizeWith`의 첫 번째 인자로 `Number` 함수를 받고 두 번째 인자로 실행 결과를 캐시할 함수를 받았다.
- `R.product`는 인자로 배열을 받아 배열 내의 모든 수를 곱한 값을 반환한다.
- `R.range`는 시작점과 끝점 간의 모든 수들을 나열한 배열을 반환한다.
- `R.product(R.range(1, n + 1))`는 1에서 주어진 값(n)까지 값을 모두 곱한 `n!`을 계산한 결과를 의미한다.
- 처음 호출된 `factorial(5)`은 계산이 되어 두 번째로 받은 함수내의 `count` 값이 1증가하지만, 두 번째로 호출된 `factorial(5)`부터는 캐시된 값이 호출될 뿐, 캐시 대상으로 지정한 함수는 호출되지 않기 때문에 `count`값이 증가하지 않는다. 따라서 `factorial(5)`을 여러 번 호출해도 `count`는 1일 뿐이다.

## Reference
- https://ramdajs.com/docs/#memoizeWith
