## add
> Adds two values.
- 두 값을 더한다.

## 설명
- 두 수를 받아 그 합을 반환한다.
- 첫 번째 인자로 수를 받고 두 번째 인자로 수를 받아서 인자로 받은 두 수의 합을 반환한다.
- 인자로 Numeric의 값을 받을 수 있다. 하지만 Numeric이 아닌 다른 값을 받으면 NaN을 반환한다.

## 문법
```ts
R.add(a, b): Number
```
- 인자 a, b에 대해 특별히 타입을 제한하지 않는 것은 Numeric의 경우 계산을 하지만 그렇지 않으면 NaN을 반환하기 때문이다.

## 표현
```
Number → Number → Number
```
- `Number →`: 첫 번째 인자로 수를 받는다.
- `→ Number →`: 두 번째 인자로 수를 받는다.
- `→ Number`: 함수를 평가할 때도 수를 반환한다.

## 예제
```
R.add(2, 3);       //=>  5
R.add(7)(10);      //=> 17
```

## Reference
- https://ramdajs.com/docs/#add
