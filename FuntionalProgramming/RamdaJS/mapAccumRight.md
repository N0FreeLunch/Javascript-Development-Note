## mapAccumRight
> The mapAccumRight function behaves like a combination of map and reduce; it applies a function to each element of a list, passing an accumulating parameter from right to left, and returning a final value of this accumulator together with the new list.

> Similar to mapAccum, except moves through the input list from the right to the left.

> The iterator function receives two arguments, acc and value, and should return a tuple [acc, value].

## 설명
- `mapAccum`와 리스트 순회 방향을 반대로 하는 것 이외에는 동일한 역할을 하는 함수이다.

## 표현
```
((acc, x) → (acc, y)) → acc → [x] → (acc, [y])
```

## 예제
```
const digits = ['1', '2', '3', '4'];
const appender = (a, b) => [b + a, b + a];

R.mapAccumRight(appender, 5, digits); //=> ['12345', ['12345', '2345', '345', '45']]
```
- 초기값 `5`와 뒤에서 부터 원소를 순차 대입하는 mapAccumRight 함수이므로`'4'`를 받는다. `(5,'4') => ['4' + 5, '4' + 5]`이므로 누적값 `'45'`와 남기는 값 `'45'`이 된다.
- 전달 받은 값은 `'45'`, 원소는 `'3'`이므로 `('45', '3') => ['3'+'45', '3'+'45']`이므로 누적값 `'345'`, 남기는 값 `'345'`이 된다.
- 전달 받은 값은 `'345'`, 원소는 `'2'`이므로 `('345', '2') => ['2'+'345', '2'+'345']`이므로 누적값 `'2345'`, 남기는 값 `'2345'`이 된다.
- 전달 받은 값은 '`2345`', 원소는 `'1'`이므로 `('2345', '1') => ['1'+'2345', '1'+2345]`이므로 누적값 `'12345'`, 남기는 값 `'12345'`가 된다.

## Reference
- https://ramdajs.com/docs/#mapAccumRight
