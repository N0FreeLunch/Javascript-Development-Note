## minBy
> Takes a function and two values, and returns whichever value produces the smaller result when passed to the provided function.
- 하나의 함수와 두 값을 받아서 어느 한 쪽의 값을 반환한다. 이 때 어느 한 쪽의 값을 반환할지는 주어진 함수에 전달된 결과가 더 작은 쪽의 값으로 결정된다.

## 설명

## 표현
> Ord b => (a → b) → a → a → a

## 예제
```js
//  square :: Number -> Number
const square = n => n * n;

R.minBy(square, -3, 2); //=> 2

R.reduce(R.minBy(square), Infinity, [3, -5, 4, 1, -2]); //=> 1
R.reduce(R.minBy(square), Infinity, []); //=> Infinity
```

## Reference
- https://ramdajs.com/docs/#minBy
