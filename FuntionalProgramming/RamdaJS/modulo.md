## modulo
> Divides the first parameter by the second and returns the remainder. Note that this function preserves the JavaScript-style behavior for modulo. For mathematical modulo see mathMod.

## 설명

## 표현
```js
Number → Number → Number
```

## 예제
```js
R.modulo(17, 3); //=> 2
// JS behavior:
R.modulo(-17, 3); //=> -2
R.modulo(17, -3); //=> 2

const isOdd = R.modulo(R.__, 2);
isOdd(42); //=> 0
isOdd(21); //=> 1
```

## Reference
- https://ramdajs.com/docs/#modulo
