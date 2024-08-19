## uncurryN
> Returns a function of arity n from a (manually) curried function.
- (수동으로) 커링된 함수로 부터 n의 인자 수를 가진 함수를 반환한다.

> Note that, the returned function is actually a ramda style curryied function, which can accept one or more arguments in each function calling.
- 반환된 함수는 실제로 ramda 스타일의 커링된 함수라는 것에 주목하자. 커링된 함수는 각각의 함수의 호출에서 (함수의 호출은 `()`으로 함수를 실행하는 것을 의미) 하나 또는 더 많은 인자를 받을 수 있다.

> See also curry, curryN.

### 설명
- 수동으로 커링된 함수라는 개념이 중요한데, `const addFour = a => b => c => d => a + b + c + d`의 코드를 보면, 인자를 하나 받고 받환된 함수가 인자를 하나 받고 반환된 함수가 인자를 하나 받아 4개의 인자를 받았을 때 평가하는 함수이다. 특별한 커링 알고리즘 없이 자바스크립트의 함수 구조를 통해서 인자를 나눠 받는 방식을 수동으로 커링된 함수라고 부른다.
- 수동으로 커링된 함수를 RamdaJS 스타일의 커링된 함수로 바꾼다. 따라서 한 번 함수가 평가 될 때 인자를 원하는 대로 받을 수 있도록 만든다.
- 특이한 점은 uncurry 함수는 반환된 함수가 갖는 인자의 수 N 값을 받아야 한다는 것이다. 이는 최종 반환 값이 함수인 경우, 계속 uncurry 될 수 있기 때문에 원하는 지점에서는 함수로 반환 받기 위한 방식으로 지정된 것으로 보인다.
- 이름이 `uncurryN`인데, 커링된 함수를 커링되지 않은 함수로 바꾸는 것이 아니라, `R.curry` 정해진 수의 인자를 받는 함수를 커링하는 것과 달리, 수동으로 커링된 함수를 RamdaJS 스타일의 커링된 함수로 만들기 위해서는 어느 정도의 인자를 받아야 할지 자바스크립트의 함수로는 파악하기 불가능한 부분이 있어 보인다. 내부적으로는 n개의 `R._`를 채워서 최종적으로 커링된 함수를 반환하는 방식으로 보인다.

### 표현
```
Number → (a → b → c … → z) → ((a → b → c …) → z)
```
- `Number →`: 반환된 함수가 갖는 인자의 수를 의미한다.
- `→ (a → b → c … → z) →`: 두 번째 인자로 함수를 받는데, 이 함수는 수동으로 커링된 함수이다. `a → b → c … →` 인자를 하나씩 받아 반환값으로 인자를 받는 함수로 요구하는 모든 인자를 다 받았을 때는 반환값 `→ z`를 갖는 함수이다.
- `→ ((a → b → c …) → z)`: 2번째 인자로 받은 함수가 ramda 식으로 커링된 함수가 된다. 두 번째 인자의 표기와 달리 `(a → b → c …)`으로 한 번에 인자를 받을 수 있다는 의미의 표현 방식이 추가 되었다.

### 예제
```js
const addFour = a => b => c => d => a + b + c + d;

const uncurriedAddFour = R.uncurryN(4, addFour);
uncurriedAddFour(1, 2, 3, 4); //=> 10
```
- `addFour`은 a, b, c, d 네 개의 인자를 받기 전에는 함수를 평가한 결과는 나머지 인자를 하나씩 순서대로 받을 수 있는 함수가 반환되는 형태이다. `addFour(1)(2)(3)(4)`의 형태로 모든 인자를 하나씩 받은 후에야 평가된다. 커링과 달리, 인자 여럿을 한 번에 받지는 않는다.
- `R.uncurryN(4, addFour)` 부분은 `R.uncurryN` 함수에 의해 인자를 4개 받을 때 까지의 대상을 커링한다. `uncurriedAddFour`는 커링이 되어 있기 때문에, 다음과 같은 인자를 함께 받고 나눠 받는 모든 패턴을 사용할 수 있다.
```js
uncurriedAddFour(1, 2, 3, 4);
uncurriedAddFour(1)(2, 3, 4);
uncurriedAddFour(1, 2)(3, 4);
uncurriedAddFour(1, 2, 3)(4);
uncurriedAddFour(1)(2, 3)(4);
uncurriedAddFour(1, 2)(3)(4);
uncurriedAddFour(1)(2)(3)(4);
```

## Referneces
- https://ramdajs.com/docs/#uncurryN
