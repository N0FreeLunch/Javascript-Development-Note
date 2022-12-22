## mapAccum
> The mapAccum function behaves like a combination of map and reduce; 
- mapAccum 함수는 map 함수와 reduce 함수의 조합으로 만들어졌다.

> it applies a function to each element of a list, passing an accumulating parameter from left to right, and returning a final value of this accumulator together with the new list.
- mapAccum 함수는 리스트의 각 원소에 적용이 되며 주어진 리스트의 원소를 왼쪽에서 오른쪽으로 차례대로 적용할 때 reduce 로직에 의해 누적되는 값을 전달한다. 최종적으로 반환되는 값은 새로운 리스트를 반환함과 동시에 누적된 값도 반환한다.

> The iterator function receives two arguments, acc and value, and should return a tuple [acc, value].
- mapAccum에 의해 리스트의 원소를 순회 적용할 때 순회함수는 두 개의 인자를 받는데 reduce 로직에 의해 누적되어 전달되는 값과 map 로직에 의해 순회 차례에 해당하는 리스트의 원소값이다. 그리고 이 순회 함수의 반환 형식은 `[누적값, 값]`이 되어야 한다.

## 설명

## 표현
```
((acc, x) → (acc, y)) → acc → [x] → (acc, [y])
```

## 예제
```
const digits = ['1', '2', '3', '4'];
const appender = (a, b) => [a + b, a + b];

R.mapAccum(appender, 0, digits); //=> ['01234', ['01', '012', '0123', '01234']]
```

## Reference
- https://ramdajs.com/docs/#mapAccum
