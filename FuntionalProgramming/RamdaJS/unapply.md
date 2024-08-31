## unapply
> Takes a function fn, which takes a single array argument, and returns a function which:
- 함수 fn을 받는다. fn은 단일 배열을 인자로 받는다. 그리고 다음과 같은 함수를 반환한다.

> takes any number of positional arguments;
- 어떠한 갯수의 인자라도 받을 수 있다.

> passes these arguments to fn as an array; and returns the result.
- 이들 인자는 fn 함수의 배열 인자로 전달된다. 그리고 fn 함수가 배열 인자를 받아 반환한 결과를 반환한다.

> In other words, R.unapply derives a variadic function from a function which takes an array. R.unapply is the inverse of R.apply.
- 달리 말하면, R.unapply 함수는 배열을 받는 함수로 부터 가변 함수를 만들어내는 함수이다. R.unapply는 (가변 함수를 하나의 배열을 받는 고정 길이 인수 함수로 변환하는) R.apply 함수의 반대 역할의 함수이다.

> See also apply.

### 설명
- 하나의 배열을 인자로 받는 함수를 배열의 원소를 인자로 받는 함수로 변환한다.
- 이 때 변환된 결과는 가변 함수이기 때문에 인자를 무한정 받을 수 있다. 따라서 커링이 되지 않으며, 한 번에 인자를 받은 만큼의 값이 함수의 평가에 적용된다.

### 표현
```
([*…] → a) → (*… → a)
```
- `([*…] → a) →`: 첫 번째 함수를 받는데, 이 함수는 인자로 임의의 타입(`*`)을 임의의 갯수(`…`) 만큼을 가진 배열을 인자로 받아 단일 타입(`a`) 결과 값을 반환하는 함수이다.
- `→ (*… → a)`: 첫 번째 인자로 받은 함수가 인자로 배열을 받았다면 반환된 함수는 배열로 받은 원소를 함수의 인자로 받을 수 있도록 변환한 함수이다.

### 예제
```js
R.unapply(JSON.stringify)(1, 2, 3); //=> '[1,2,3]'
```
- [JSON.stringify](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) 함수는 값을 받아서 json 스트링으로 변환한다. 이 때 값을 하나 받아서 해당 값을 json 포멧의 문자열 방식으로 변환한다.
- 인자로 하나의 값을 받기 때문에, 인자를 나눠서 받기 위해서 `R.unapply` 함수로 새로운 함수를 만들었다. 원래는 `[1,2,3]`의 값을 받지만, 새롭게 만들어진 함수는 1, 2, 3을 따로 인자로 받는다.

## References
- https://ramdajs.com/docs/#unapply
