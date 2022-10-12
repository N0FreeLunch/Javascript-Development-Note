## isNil
> Checks if the input value is null or undefined.
- 주어진 값이 null 또는 undefined인지 체크한다.

## 표현
```
* → Boolean
```
- `* →` 임의의 종류의 어떤 값을 받는다.
- `→ Boolean` 첫 번째 인자로 받은 값이 `null` 또는 `undefined`인지 확인한다. 

## 설명
- 주어진 값이 정의되지 않았는지 확인한다.
- 정의되지 않았다면 참, 정의되었다면 거짓을 반환한다.
- 자바스크립트에서 `null`과 `undefiend`를 정의할 수 있지만 타입 자체로는 정의되지 않은 것으로 본다.

## 예제
```
R.isNil(null); //=> true
R.isNil(undefined); //=> true
R.isNil(0); //=> false
R.isNil([]); //=> false
```

## Reference
- https://ramdajs.com/docs/#isNil
