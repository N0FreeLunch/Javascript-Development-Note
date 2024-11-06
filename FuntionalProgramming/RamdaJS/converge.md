## converge

> Accepts a converging function and a list of branching functions and returns a new function. 
- 수렴 함수(converging function)와 분기 함수(branching functions) 리스트를 (인자로) 받아 새로운 함수를 반환한다.
> The arity of the new function is the same as the arity of the longest branching function.
- 새로운 함수의 (평가를 위해 필요한) 인자의 수는 가장 긴 분기 함수의 인자의 수와 같다.
> When invoked, this new function is applied to some arguments, and each branching function is applied to those same arguments.
- 몇몇의 인자가 적용되어 (반환된) 새로운 함수가 호출되면, 각각의 분기 함수에 동일한 인자들이 적용된다.
> The results of each branching function are passed as arguments to the converging function to produce the return value.
- 각각의 분기 함수(branching function)의 결과는 수렴 함수(converging function)의 인자로 전달되어 반환 값을 생성한다.

### 설명
```
R.converge(수렴 함수, [분기 함수의 리스트])(분기 함수에 전달할 인자들)
```
- 일반적으로 연산 함수는 함수를 인자로 받지 않고 값을 인자로 받아서 값의 결과를 연산한 결과를 돌려 준다. 인자로 값을 받는 연산 함수의 인자에 값 대신 함수를 전달하는 방식의 함수를 만들기 위해 사용한다. 인자를 값 대신 함수로 전달하는 것은 각 연산 함수가 어떤 대상을 인자로 받는지 알기 쉽게 만들어 주는 장점이 있다.
- 예를 들어 `R.converge(R.divide, [R.sum, R.length])`인 경우, `R.divide`의 첫 번쩨 인자로는 `R.sum`으로 인자로 들어 온 모든 값을 합산한 결과를, 두 번째 인자로는 `R.length`으로 인자로 들어 온 값의 길이값을 사용하라는 의미로 함수가 어떻게 구성되어 있는지 쉽게 알 수 있게 해 준다.
- 여기서는 연산의 예를 들었지만, 연산 뿐만 아닌 다양한 함수에 적용 가능한 원리이므로 연산 함수 부분은 수렴 함수라고 부르고, 수렴 함수의 인자로 전달하기 위한 값을 만드는 함수를 수렴 함수에 의해 하나로 합쳐지는 함수를 나뭇가지가 줄기로 합쳐지는 것에 비유하여 가지 함수 또는 분기 함수 (branching function)라고 부른다.
- 최종적으로 반환된 함수는 인자를 받을 것이다. 이 인자는 수렴 함수에 전달할 결과를 만들기 위한 함수를 통해 값을 반환 해야 하므로, 각각의 분기 함수는 반환된 함수가 받는 인자를 그대로 받아야 하므로 모든 분기 함수는 동일한 인자를 전달 받는다.
- 수렴 함수가 평가 되기 위해서는 수렴함수가 받는 인자를 충족해야 하므로, 일반적으로는 수렴 함수가 평가되기 위한 인자의 갯수 만큼, 분기 함수를 전달 받아야 한다.

### 문법
```
R.converge(after, functions): function
```
> `after`: A function. after will be invoked with the return values of fn1 and fn2 as its arguments.
- `after`: 함수이다. 이 함수는 (분기 함수 리스트(functions)의) fn1 함수와 fn2 함수의 반환 값을 인자로 하여 호출된다.
> `functions`: A list of functions.
- `functions`: 함수의 리스트
> Returns function A new function.
- 새로운 함수를 반환한다.

### 표현
```
((x1, x2, …) → z) → [((a, b, …) → x1), ((a, b, …) → x2), …] → (a → b → … → z)
```
- `(x1, x2, …) → z) →`: 첫 번째 인자로 최종적으로 두 번째 함수들에 나열된 함수들의 결과를 종합하여 받을 함수를 받는다. 인자로 `x1`, `x2`, `x3`...를 받는 것은 두 번째 함수 리스트의 반환 값을 받기 때문에 두 번째 함수들의 반환 값의 타입과 동일하며 그 나열 순서도 동일하다. 이 함수는 `z`라는 종류의 결과 값을 만드는데, 최종적으로 반환된 함수의 결과 값과 동일한 종류의 값이다.
- `→ [((a, b, …) → x1), ((a, b, …) → x2), …] →`: 두 번째 인자로는 첫 번째 인자의 함수에 인자로 전달할 값을 만들기 위한 함수를 나열한 것으로 각각의 나열된 순서대로 각각의 함수의 반환 값이 첫 번째 함수의 인자로 전달된다. `((a, b, …) → x1)`, `((a, b, …) → x2)`을 보면 동일한 타입의 인자들(`(a, b, …)`)을 받는데, 이는 반환된 함수 `(a → b → … → z)`가 받는 인자 `a → b → …`를 받기 때문에 동일한 종류의 인자를 전달 받는다. 그리고 각각의 함수의 반환 값은 그대로 첫 번째 인자인 함수의 인자로 전달되므로 `((x1, x2, …) → z)`의 인자와 동일한 종류인 `x1`, `x2`, `x3`...가 반환되는 것을 알 수 있다.
- `→ (a → b → … → z)`: 최종적으로 반환된 함수는 인자를 전달 받아, 두 번째 함수 리스트에 전달하고, 두 번째 함수 리스트의 함수 각각에 인자가 전달되어 반환된 결과 값이 첫 번째 함수의 인자로 할당되어 첫 번째 함수가 평가된 결과가 반환되는 표현이다.

### 예제
```js
const average = R.converge(R.divide, [R.sum, R.length])
average([1, 2, 3, 4, 5, 6, 7]) //=> 4
```
- `R.divide`함수는 첫번째 인자로 피제수를 받고 두 번째 인자로 제수를 받아서 피제수/제수 연산한 결과를 반환하는 함수이다.
- `R.converge`를 사용하여 `R.divide` 함수에 인자를 직접할당하지 않고 첫 번째 인자는 배열의 첫 번째 함수의 결과를 두 번째 인자는 배열의 두 번째 함수의 결과를 받는 식으로 함수의 인자를 배열의 함수가 평가된 결과 값으로 할당하는 방식을 사용할 수 있게 한다. `R.converge(대상 함수, [대상 함수의 인자에 할당하기 위한 값을 만들 함수들])`이다. (대상 함수는 수렴 함수이고, '대상함수의 인자에 할당하기 위한 값을 만들 함수들'은 분기 함수들이다.)
- `[1, 2, 3, 4, 5, 6, 7]`이란 값이 주어지면, `R.sum([1, 2, 3, 4, 5, 6, 7])`의 결과가 `R.divide`의 첫 번째 인자로 할당되고, `R.length([1, 2, 3, 4, 5, 6, 7])`의 결과가 `R.divide`의 두 번째 인자로 할당된다.
- `R.sum([1, 2, 3, 4, 5, 6, 7])`의 결과는 `28`, `R.length([1, 2, 3, 4, 5, 6, 7])`의 결과는 `7`이므로 `R.divide(28, 7)`의 결과는 `4`이다.

```js
const strangeConcat = R.converge(R.concat, [R.toUpper, R.toLower])
strangeConcat("Yodel") //=> "YODELyodel"
```
- `R.concat`함수는 인자로 받은 두 배열 형식의 타입(문자열, 배열 등)을 가진 대상의 모든 원소가 들어 있는 배열 형식으로 합친 결과를 반환한다. 이때 결합 결과는 문자열이면 문자열로, 배열이면 배열로 동일한 타입이다.
- `R.toUpper("Yodel")`의 결과가 `R.concat`의 첫 번째 인자로 할당되고, `R.toLower("Yodel")`의 결과가 `R.concat`의 두 번째 인자로 할당된다.
- 따라서 결과는 `R.concat("YODEL", "yodel")`인 `"YODELyodel"`가 된다.

## References
- https://ramdajs.com/docs/#converge
- https://github.com/ramda/ramda/blob/master/test/converge.js
- https://github.com/ramda/types/blob/develop/types/converge.d.ts
