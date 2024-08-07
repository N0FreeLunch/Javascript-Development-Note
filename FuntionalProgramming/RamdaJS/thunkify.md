## thunkify
> Creates a thunk out of a function. A thunk delays a calculation until its result is needed, providing lazy evaluation of arguments.
- 함수로 부터 thunk를 생성한다. thunk란 결과가 필요할 때까지 계산을 지연시켜 인자들에 대한 지연 평가를 제공한다.

> See also partial, partialRight.

### 설명
- 어떤 함수의 인자를 미리 세팅 하여 인자 없이 실행하는 것으로 결과 값을 얻는 함수를 만들도록 한다.
- 첫 번째 인자로는 임의의 함수를 하나 받아서 두 번째 인자 부터 n+1 번째 인자까지 첫 번째 인자에 넣을 인자 n개를 받아 함수를 반환한다. 이 함수는 ()으로 평가하는 것으로 첫 번째 인자로 받은 함수에 두 번째 부터 n+1번째까지의 인자를 전달한 결과값을 반환한다.
- 이러한 내포된 함수를 평가하기 위해 필요한 인자를 모두 포함하고 있는 함수를 thunk 함수라고 한다. 그리고 어떤 함수를 thunk 함수로 만드는 과정을 thunkify라고 한다. thunkify 함수는 함수를 thunk 함수로 만드는 함수를 의미한다.

### 표현
```
((a, b, …, j) → k) → (a, b, …, j) → (() → k)
```
- `((a, b, …, j) → k) →`: 첫 번째 인자로 하나의 인자를 반환하는 임의의 함수를 받는다.
- `→ (a, b, …, j) →`: 두 번째 인자 부터는 첫 번째 함수의 인자로 전달 할 수 있는 인자 리스트를 받는다. 전달할 인자의 수에 따라 두 번째 뿐만 아니라 세 번째, 네 번째, .... 계속 인자를 받는다. 이 때 () 표기로 인자들이 나열되어 있는데 이는 인자들을 커링으로 나눠서 받는 것이 아닌 한 번에 받는 것을 의미한다.
- `→ (() → k)`: 반환 값으로 인자를 받지 않고 평가되는 함수를 반환하는데, 이 함수는 첫 번째 함수를 실행하기 위한 모든 인자를 포함하고 있는 함수로 인자 없이 함수를 평가하는 것으로 첫 번째 인자에 두 번째 인자부터 마지막 인자까지의 값을 전달한 결과값을 반환한다. 반환된 함수를 평가한 최종값의 타입을 k으로 표기하고 있는데, 이는 첫 번째 인자의 함수의 반환 타입과 동일한 것으로 첫 번째 인자의 함수에 인자를 전달한 결과 값과 동일한 값이기 때문이다.

### 예제
```js
R.thunkify(R.identity)(42)(); //=> 42
R.thunkify((a, b) => a + b)(25, 17)(); //=> 42
```
- `R.identity` 함수를 사용하여 thunk를 생성한다. 생성된 thunk인 `R.thunkify(R.identity)`는 인자 42를 받고, 함수를 반환한다. `R.thunkify(R.identity)(42)`가 하나의 함수가 되고, 이 함수는 다시 평가되어야 함수의 결과값을 반환한다. 최종 평가시에는 이미 함수를 평가하는데 필요한 모든 조건이 갖춰져 있기 때문에 인자로 아무런 값도 받지 않는다.
- `(a, b) => a + b` 함수를 사용하여 thunk를 생성한다. 생성된 thunk인 `R.thunkify((a, b) => a + b)`는 인자 `(25, 17)`를 받고, 함수를 반환한다. `R.thunkify((a, b) => a + b)(25, 17)`가 하나의 함수가 되고,이 함수는 다시 평가되어야 함수의 결과값을 반환한다. 최종 평가시에는 이미 함수를 평가하는데 필요한 모든 조건이 갖춰져 있기 때문에 인자로 아무런 값도 받지 않는다.

## Reference
- https://ramdajs.com/docs/#thunkify
