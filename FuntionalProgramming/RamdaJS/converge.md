## converge
> Accepts a converging function and a list of branching functions and returns a new function. 
- 수렴(converging) 함수는 분기(branching) 함수 리스트를 인자로 받아 새로운 함수를 구성합니다.
> The arity of the new function is the same as the arity of the longest branching function. 
- 새로운 함수의 피연산자는 분기함수의 피연산자와 같습니다.
> When invoked, this new function is applied to some arguments, and each branching function is applied to those same arguments.
- `R.converge`에 의해 만들어진 수렴(converging) 함수가 호출되면, 호출될 때 전달된 인자가 각 분기함수의 인자로 전달됩니다. 각 분기 함수는 똑같은 인자를 전달 받습니다.
> The results of each branching function are passed as arguments to the converging function to produce the return value.
- 각 분기 함수의 결과는 수렴함수의 인자로 전달되며 수렴함수는 이들 인자를 연산한 결과 값을 반환합니다.

## 표현
```
((x1, x2, …) → z) → [((a, b, …) → x1), ((a, b, …) → x2), …] → (a → b → … → z)
```
- `(x1, x2, …) → z) →` 첫 번째 인자로 연산을 할 대상 함수를 받는다.  `x1`, `x2`, `x3`... 의 인자를 받으면 `z`라는 결과 값을 만드는 함수를 받는다.
- `→ [((a, b, …) → x1), ((a, b, …) → x2), …] →` 두 번째 인자로는 첫 번째 인자에 평가한 결과 값을 할당할 함수들을 나열한 배열을 받는다. `((a, b, …) → x1)`, `((a, b, …) → x2)`을 보면 동일한 타입의 인자들(`(a, b, …)`)을 받아서 대상함수의 인자인  `x1`, `x2`, `x3`...을 반환하는 것을 알 수 있다.
- `→ (a → b → … → z)` 세 번째 인자로는 두 번째 인자의 배열에 나열된 함수의 인자로 들어갈 인자리스트와 동일한 타입이다.

## 설명
```
R.converge(대상함수, [대상 함수의 인자에 결과 값을 넣을 함수])
```
- 일반적으로 연산 함수는 함수를 인자로 받지 않고 값을 인자로 받아서 값의 결과를 연산한 결과를 돌려 준다.
- 인자로 값을 받는 연산 함수의 인자에 값 대신 함수를 전달하는 방식으로 함수를 만들기 위해 사용한다.
- 인자를 값 대신 함수로 전달하는 것은 각 연산 함수가 어떤 대상을 인자로 받는지 알기 쉽게 만들어 주는 장점이 있다.
- 예를 들어 `R.converge(R.divide, [R.sum, R.length])`인 경우, `R.divide`의 첫 번쩨 인자로는 `R.sum`으로 인자로 들어 온 모든 값을 합산한 결과를, 두 번째 인자로는 `R.length`으로 인자로 들어 온 값의 길이값을 사용하라는 의미로 함수가 어떻게 구성되어 있는지 쉽게 알 수 있게 해 준다.
- 먼저 연산할 대상 함수를 지정하고 대상 함수의 인자에 넣을 값을 두 번째 인자의 배열에 나열한다. 이 때 대상 함수의 인자에 넣을 값을 지정하는 것은 함수가 평가 된 값이 들어간다.
- 수렴함수의 세 번째 인자로는 대상 함수를 실행하기 위한 인자를 받으며 두 번째 인장인 배열에 나열 된 각각의 함수들에 세 번째 인자를 모두에게 전달한다.
- 두 번째 인자의 함수들은 전달 받은 인자를 평가한 결과 값을 대상함수의 인자로 전달하여 연산을 수행하여 수렴함수가 평가된다.

## 예제
```
const average = R.converge(R.divide, [R.sum, R.length])
average([1, 2, 3, 4, 5, 6, 7]) //=> 4

const strangeConcat = R.converge(R.concat, [R.toUpper, R.toLower])
strangeConcat("Yodel") //=> "YODELyodel"
```
- `R.divide`함수는 첫번째 인자로 피제수를 받고 두 번째 인자로 제수를 받아서 피제수/제수 연산한 결과를 반환하는 함수이다.
- `R.converge`를 사용하여 `R.divide` 함수에 인자를 직접할당하지 않고 첫 번째 인자는 배열의 첫 번째 함수의 결과를 두 번째 인자는 배열의 두 번째 함수의 결과를 받는 식으로 함수의 인자를 배열의 함수가 평가된 결과 값으로 할당하는 방식을 사용할 수 있게 한다. `R.converge(대상함수, [대상함수의 인자에 할당하기 위한 값을 만들 함수들])`이다.
- `[1, 2, 3, 4, 5, 6, 7]`이란 값이 주어지면, `R.sum([1, 2, 3, 4, 5, 6, 7])`의 결과가 `R.divide`의 첫 번째 인자로 할당되고, `R.length([1, 2, 3, 4, 5, 6, 7])`의 결과가 `R.divide`의 두 번째 인자로 할당된다.
- `R.sum([1, 2, 3, 4, 5, 6, 7])`의 결과는 `28`, `R.length([1, 2, 3, 4, 5, 6, 7])`의 결과는 `7`이므로 `R.divide(28, 7)`의 결과는 `4`이다.
- `R.concat`함수는 인자로 받은 두 배열형식의 타입을 가진 대상의 모든 원소가 들어 있는 하나의 배열로 합친 결과를 반환한다.
- `R.toUpper("Yodel")`의 결과가 `R.concat`의 첫 번째 인자로 할당되고, `R.toLower("Yodel")`의 결과가  `R.concat`의 두 번째 인자로 할당된다.
- 따라서 결과는 `R.concat("YODEL", "yodel")`인 `"YODELyodel"`가 된다.

## Reference
- https://ramdajs.com/docs/#converge
