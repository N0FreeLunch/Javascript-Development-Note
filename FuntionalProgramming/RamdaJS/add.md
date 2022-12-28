## add
> Adds two values.
- 두 값을 더한다.

## 설명
- 두 개의 인자는 수를 받아 두 수의 합을 반환한다.
- 첫 번째 인자로 수를 받고 두 번째 인자로 수를 받아서 인자로 받은 두 수를 더한 결과를 반환한다.

## 문법
```
R.add(Number, Number)
```
리턴타입 : `Number`

## 표현
```
Number → Number → Number
```
- `Number →` 첫 번째 인자로 수를 받고
- `→ Number →` 두 번째 인자로 수를 받고
- `→ Number` 함수를 평가할 때도 수를 반환

## 예제
```
R.add(2, 3);       //=>  5
R.add(7)(10);      //=> 17
```

## Reference
- https://ramdajs.com/docs/#add
