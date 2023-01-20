## compose
> Performs right-to-left function composition. The last argument may have any arity; the remaining arguments must be unary.
- 오른쪽에서 왼쪽의 순으로 함수를 합성한다. 마지막 인자는 어떤 인자라도 받을 수 있는 것이 올 수 있으며, 나머지 인자는 하나의 인자를 취해서 평가되는 함수이어야 한다.

> Note: The result of compose is not automatically curried.
- `compose`함수를 통해서 합성된 함수는 자동적으로 커리되지 않는다.

## 설명
- 여러 개의 함수를 하나의 함수로 합성하는 기능을 한다.
- 합성된 함수의 인자로 값을 하나 받아서 오른쪽에 나열된 함수의 평가 결과를 그 옆의 왼쪽 함수의 인자로 전달하는 방식으로 주어진 함수를 평가한 결과를 내 놓는 함수이다.
- 만약 함수를 인자로 받다가 함수가 아닌 값을 받으면 해당 함수는 합성함수를 반환하지 않고 즉시 평가된다.
- 함수의 반환값은 프로그래밍 언어의 단일 값으로 취급되는 단위이다. 반환된 하나의 값을 전달해서 다음 함수가 평가 되어야 하기 때문에 나열되는 함수는 인자 하나를 받아 평가 될 수 있는 함수이어야 한다.
- 참고 : 함수가 평가되기 위해 받아야 하는 인자의 갯수를 읽컫는 말을 `arity`(애리티)라고 한다. 인자를 하나 받는 함수를 `unary`라고 부른다. (인자를 두 개 받는 함수의 인자를 `binary`, 인자를 세 개 받는 함수의 인자를 `ternary`, 인자를 받지 않는 경우를 `nullary`라고 한다.)

## 표현
```
((y → z), (x → y), …, (o → p), ((a, b, …, n) → o)) → ((a, b, …, n) → z)
```
- `((y → z), (x → y), …, (o → p), ((a, b, …, n) → o))`는 인자로 여러 함수를 받는다는 의미이다. 그런데 마지막 함수 `((a, b, …, n) → o)`를 제외하고는 인자를 하나 받아서 하나의 반환값을 만드는 함수이다. `(y → z)`, `(x → y)`, `(o → p)`. 가장 마지막 함수는 꼭 인자를 하나만 받을 필요가 없으며 여러개를 받아도 된다.
- 반환된 함수 `((a, b, …, n) → z)`는 인자 `(a, b, …, n)`를 받아서 그 결과 값인 `z`를 반환한다. 이 때 받은 인자 `(a, b, …, n)`는 첫 번재 인자세트를 받을 때 가장 마지막 함수인 `((a, b, …, n) → o))`에 전달할 수 있는 인자가 와야 한다.

## 예제
```
const classyGreeting = (firstName, lastName) => "The name's " + lastName + ", " + firstName + " " + lastName
const yellGreeting = R.compose(R.toUpper, classyGreeting);
yellGreeting('James', 'Bond'); //=> "THE NAME'S BOND, JAMES BOND"

R.compose(Math.abs, R.add(1), R.multiply(2))(-4) //=> 7
```
- `yellGreeting('James', 'Bond');`의 결과는 `"THE NAME'S BOND, JAMES BOND"``이다. 모두 대문자로 결과가 나왔다는 것은 바인딩이 되고 나서 `R.toUpper`함수가 적용되었다는 것이다.
- `R.compose(R.toUpper, classyGreeting);`에서 함수 적용 순서는 `classyGreeting`가 먼저 실행이 되고 `R.toUpper`가 실행이 되는 것. 인자로 지정된 함수를 오른쪽 부터 적용한다.
- `R.compose(Math.abs, R.add(1), R.multiply(2))`를 오른쪽에서 왼쪽으로 평가하면 2를 먼저 곱하고 1을 더하고 이 값에 절대값을 취한다이다. `(-4)`를 받으면 `|-4 x 2 + 1|`로 7이란 값이 나온다.

## Reference
- https://ramdajs.com/docs/#compose
