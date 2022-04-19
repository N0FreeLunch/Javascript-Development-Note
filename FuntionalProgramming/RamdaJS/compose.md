## compose
- R.compose()

## 설명
- 인자로 함수를 넣고 인자로 할당된 함수를 오른쪽 부터 순차적으로 적용한다.

## 표현
```
((y → z), (x → y), …, (o → p), ((a, b, …, n) → o)) → ((a, b, …, n) → z)
```
- `((y → z), (x → y), …, (o → p), ((a, b, …, n) → o))`는 인자로 여러 함수를 받는다는 의미이다. `(y → z)` 함수, `(x → y)` 함수, `…` 이런 함수 여럿, `(o → p)` 함수 `((a, b, …, n) → o)` 함수를 인자로 받는다.

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
