## apply
- Applies function fn to the argument list args. This is useful for creating a fixed-arity function from a variadic function. fn should be a bound function if context is significant.
- 함수 fn에 인자 리스트 args를 적용한다. 가변 인자를 갖는 함수에서 인자의 갯수를 고정한 함수를 생성하는데 유용하다. 컨텍스트가 중요한 경우 fn은 바인딩된 함수여야 한다.

> See also call, unapply.

### 설명
- 어떤 함수의 배열에 나열한 값을 각각의 인자로 할당하고자 할 때 사용하는 함수이다.
- 첫 번째 인자는 평가할 함수를 넣고
- 두 번째 인자는 '첫번째 인자에 지정한 함수'에 할당할 인자를 나열한 배열을 받는다.
- 배열의 원소들이 '첫번째 인자에 지정한 함수'의 첫 번째 인자에는 첫 번째 나열된 값이, 두 번째 인자에는 두 번째 나열된 값이, ... 이런식으로 배열 안의 모든 인자가 할당되어 평가된다.
- 첫 번째 인자의 함수를 가변 인자를 받는 함수를 고정 길이 인자를 받는 함수로 전환시킬 수 있다. `R.apply(fn)`으로 두 번째 인자를 받지 않는다면 커링되어 배열을 하나 받는 함수로 바꿀 수 있다.
- '컨텍스트가 중요한 경우 fn은 바인딩된 함수여야 한다.'라는 설명이 있는데, 이는 [bind](./bind.md) 함수를 참고하자. 어떤 오브젝트 context에 대해 context.fn으로 실행되는 함수는 context 안의 프로퍼티를 이용하는 경우가 있는데, this로 해당 컨텍스트 안의 값을 접근하기 위해서는, `R.apply(context.fn)`를 그냥 쓰지 않고, `R.apply(bind(fn, context))`와 같은 코드를 사용해 줘야 한다.

### 문법
```
R.apply(fn, args): *
```
- fn: The function which will be called with args
- args: The arguments to call fn with
- Returns * result The result, equivalent to `fn(...args)`

### 표현
```
(*… → a) → [*] → a
```
- `(*… → a) →`: 임의의 타입의 인자들을 받아서 단일 타입의 결과를 반환하는 함수를 의미한다. 이 때 함수가 받을 수 있는 인자는 고정 길이가 아닌 가변 인자일 수 있다.
- `→ [*] →`: 첫번째 인자로 지정된 함수의 인자 리스트를 갖는 배열을 지정한다. 인자 각각은 함수의 인자로 전달할 수 있는 다양한 타입의 값이 될 수 있기 때문에 `*`이다.
- `→ a`: 두 번째 인자로 지정한 배열의 원소를 첫 번째 인자의 함수의 인자에 넣어서 평가된 결과를 반환한다. `(*… → a)`에서 지정한 함수의 결과값을 타입으로 하는 결과가 반환된다.

### 예제
```js
const nums = [1, 2, 3, -99, 42, 6, 7];
R.apply(Math.max, nums); //=> 42
```
- 먼저 max 함수를 살펴보면
```
console.log(Math.max(1, 3, 2));
// expected output: 3

console.log(Math.max(-1, -3, -2));
// expected output: -1
```
- `Math.max` 함수는 주어진 인자 리스트에서 가장 높은 수를 선택한다.
- `R.apply`의 두 번째 인자에는 인자로 넣을 대상 리스트를 배열형식으로 받는다.
- 두 번째 인자로 받은 배열의 원소를 순차적으로 첫번째 인자의 함수의 인자에 넣어 실행한다.

## References
- https://ramdajs.com/docs/#apply
- https://github.com/ramda/ramda/blob/master/test/apply.js
- https://github.com/ramda/types/blob/develop/types/apply.d.ts
