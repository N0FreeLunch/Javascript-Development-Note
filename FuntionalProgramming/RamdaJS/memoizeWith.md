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
- `Number`는 주어진 인자를 수로 바꾸는 함수이다.
- `R.memoizeWith`의 첫 번째 인자로 `Number` 함수를 받고 두 번째 인자로 실행 결과를 캐시할 함수를 받았다.
- `R.product`는 인자로 배열을 받아 배열 내의 모든 수를 곱한 값을 반환한다.
- `R.range`는 시작점과 끝점 간의 모든 수들을 나열한 배열을 반환한다.
- `R.product(R.range(1, n + 1))`는 1에서 주어진 값(n)까지 값을 모두 곱한 `n!`을 계산한 결과를 의미한다.

## Reference
- https://ramdajs.com/docs/#memoizeWith
