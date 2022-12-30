## and
> Returns the first argument if it is falsy, otherwise the second argument.
- 첫 번째 거짓이라면 첫 번째 인자를 반환하고 첫 번째 인자가 참이라면 두 번째 인자를 반환한다. 
> Acts as the boolean and statement if both inputs are Booleans.
- 만약 입력된 두 인자가 불리언 타입이면 불리언 and 연산자 처럼 동작한다.
> See also both, or.

## 설명
- 두 인자를 받아서 첫 번째 인자를 불리언 타입으로 자동형변환한 값이 참이면 첫 번째 인자를 반환하고 거짓이면 두 번째 인자를 반환한다.

## 문법
```
R.and(anyToBeConvertedBoolean, any)
```
반환값 : 인자로 받은 두 값 중 하나가 반환된다.

## 표현
```
a → b → a | b
```
- `a →` 인자 a를 받고
- `b →` 인자 b를 받아서
- `→ a | b` a 또는 b 인자를 반환한다.

## 예제
```
R.and(true, true); //=> true
R.and(true, false); //=> false
R.and(false, true); //=> false
R.and(false, false); //=> false
```
- 위 예제를 보면 실제 불리언 연산에서의 and 연산자와 정의는 다르지만 2개의 인자를 불리언 타입으로 받을 경우 동일한 결과를 만드는 것을 알 수 있다.

## Reference
- https://ramdajs.com/docs/#and
