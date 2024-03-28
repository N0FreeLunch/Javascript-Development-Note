## partialRight
> Takes a function f and a list of arguments, and returns a function g. When applied, g returns the result of applying f to the arguments provided to g followed by the arguments provided initially.
- 함수 f와 인자 리스트 하나를 받아 함수 g를 반환한다. 함수 f에 인자 리스트가 적용되어 만들어진 함수 g는 f에 인자가 적용된 것으로, 이들 인자는 초기 g 함수에 제공되어 있다.

> See also partial.

### 설명
- 주어진 인자 리스트의 마지막 원소 부터 함수의 마지막 파라메터 부터 순차적으로 매칭하여 주어진 인자 리스트를 미리 포함하고 있는 함수를 반환한다.
- 예를 들어 함수의 파라메터가 (a, b, c, d, e, f)라면, 인자 리스트로 `[1,2,3]`가 매칭이 되면 `c, d, e`에 값이 매칭되는 형태이다.
- `partial` 함수가 주어진 인자 리스트의 원소를 순차적으로 함수의 첫 번째 인자 부터 순차적으로 매칭하는 반면, `partialRight` 함수는 주어진 인자 리스트의 원소를 마지막 부터 순차적으로 함수의 마지막 인자 부터 순서대로 매칭한다.

### 표현
```
((a, b, c, …, n) → x) → [d, e, f, …, n] → ((a, b, c, …) → x)
```
- `((a, b, c, …, n) → x) →` : 첫 번째 인자로 함수 하나를 받는다. 이 함수는 파라메터로 `a, b, c, …, n`를 가지며, 모든 인자를 다 받으면 평가되어 x를 반환한다.
- `→ [d, e, f, …, n] →` : 두 번째 인자로, 첫 번째 인자의 함수의 인자에 적용할 인자 리스트를 받는다. `a, b, c`가 빠진 `d, e, f, …, n`를 인자로 받는데, `d, e, f, …, n`가 적용된 함수를 반환하게 된다.
- `→ ((a, b, c, …) → x)` : 이미  `d, e, f, …, n`가 적용되어 있는 함수이기 때문에 첫 번째 인자로 받은 함수가 평가되기 위한 조건인 나머지 인자 `a, b, c, …`를 받으면 평가가 되어 첫 번째 인자로 받은 함수의 반환 결과와 동일한 결과를 반환한다.

### 예제
```js
const greet = (salutation, title, firstName, lastName) =>
  salutation + ', ' + title + ' ' + firstName + ' ' + lastName + '!';

const greetMsJaneJones = R.partialRight(greet, ['Ms.', 'Jane', 'Jones']);

greetMsJaneJones('Hello'); //=> 'Hello, Ms. Jane Jones!'
```
- `greet`라는 함수는 4개의 인자(`salutation, title, firstName, lastName`)를 받는다. `partialRight`를 사용하여 인자를 지정할 때, 인자 리스트의 마지막 원소 부터 마지막 인자 부터 차례로 매칭된다.
- `R.partialRight(greet, ['Ms.', 'Jane', 'Jones'])`에서 인자 리스트로 `['Ms.', 'Jane', 'Jones']`를 받고, 마지막 원소는 마지막 인자에 매칭되므로 `'Jones'`는 `lastName` 파라메터에 매칭이 되고, `'Jane'`는 `firstName` 파라메터에 매칭되고, `'Ms.'`는 `title`에 매칭된다. 그리고 이들 인자를 이미 포함하고 있는 함수 `greetMsJaneJones`를 반환한다.
- `greetMsJaneJones`는 `greet` 함수가 평가 되기 위해 필요한 4개의 인자 중에서 3개를 이미 받은 상태로 아직 받지 않은 나머지 인자인 `salutation` 인자를 받아 평가된다.

## Reference
- https://ramdajs.com/docs/#partialRight
