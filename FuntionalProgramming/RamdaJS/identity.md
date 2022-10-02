## identity
> A function that does nothing but return the parameter supplied to it. Good as a default or placeholder function.
- 아무것도 하지 않는 함수이다. 파라메터로 주어진 값을 그대로 반환하는 함수이다. 

## 표현
```
a → a
```
- `a →` 넣은 인자를
- `→ a` 그대로 반환한다.

## 설명
- 인자의 값을 그대로 반환하는 함수이다.
- 오브젝트의 경우는 동일한 참조를 반환한다.

## 예제
```
R.identity(1); //=> 1

const obj = {};
R.identity(obj) === obj; //=> true
```

## Reference
- https://ramdajs.com/docs/#identity
