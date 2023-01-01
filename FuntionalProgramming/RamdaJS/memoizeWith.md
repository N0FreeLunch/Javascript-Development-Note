## memoizeWith
> Creates a new function that, when invoked, caches the result of calling fn for a given argument set and returns the result. Subsequent calls to the memoized fn with the same argument set will not result in an additional call to fn; instead, the cached result for that set of arguments will be returned.

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

## Reference
- https://ramdajs.com/docs/#memoizeWith
