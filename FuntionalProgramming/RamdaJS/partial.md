## partial
> Takes a function f and a list of arguments, and returns a function g. When applied, g returns the result of applying f to the arguments provided initially followed by the arguments provided to g.
- partial이란 함수는 첫 번째 인자로 함수 f를 받고 두 번째 인자로 인자의 리스트를 받아서 함수 g를 리턴한다. partial 함수에 의해 반환된 함수 g는, 함수 f에 partial의 두 번째 인자로 제공된 인자들을 미리 세팅한 함수 g를 반환한다.

### 설명
- 함수와 인자 리스트를 받아 함수의 커링 여부에 상관 없이 주어진 인자를 머금고 있는 함수를 생성한다.
- 예를 들어 함수가 커링되면 `f(a,b,c)`는 `f(a)(b)(c)`가 될 것이다. `f(a)(b)`란 함수는 인자 `c`를 받아 같은 결과값을 반환한다. `R.partial(f, [a,b])`가 g라는 함수를 만든다고 하자. `g(c)`는 `f(a)(b)`에 `(c)`를 인자로 넣은 것과 같은 결과 값을 얻는다.
- 커링이란 평가에 필요한 모든 인자들이 채워질 때까지 모든 인자를 나누어 받고 지정한 수의 인자를 받았을 때 평가가 되는 방식이지만, partial은 초기에 지정한 인자만을 미리 세팅하고 평가에 필요한 나머지 인자를 받는 방식이다. f가 커링 되어 있다면 인자의 일부가 미리 세팅된 g는 인자를 하나씩 받을 수 있지만, f가 커링되어 있지 않다면 g는 평가에 필요한 모든 인자를 한 번에 받아야 한다.

### 표현
```
((a, b, c, …, n) → x) → [a, b, c, …] → ((d, e, f, …, n) → x)
```
- `((a, b, c, …, n) → x) →` 첫 번째 인자로는 함수를 받는다.
- `→ [a, b, c, …] →` 두 번째 인자로는 첫 번째 인자로 받은 함수의 인자에 할당할 값을 리스트로 받는다. 이 때 첫 번째 인자로 받는 함수의 인자의 형식이 `(a, b, c, …, n)`인데 이 인자에 매칭되는 값을 인자 리스트로 받으므로 `[a, b, c, …]`가 되며, 첫 번째 인자로 받는 함수의 인자가 모두 채워지지 않고 부분적으로 채워진 함수를 반환하는 목적이므로 `n`까지 받지는 않도록 표기가 되어 있다.
- `((d, e, f, …, n) → x)` 반환된 함수는 첫 번째 함수에 두 번째 인자의 `a, b, c`라는 값을 미리 세팅한 함수이므로 그와 다른 나머지 인자를 채워 넣는다고 `(d, e, f, …, n)`라는 표기를 해 주었다.

### 예제
```js
const multiply2 = (a, b) => a * b;
const double = R.partial(multiply2, [2]);
double(3); //=> 6

const greet = (salutation, title, firstName, lastName) =>
  salutation + ', ' + title + ' ' + firstName + ' ' + lastName + '!';

const sayHello = R.partial(greet, ['Hello']);
const sayHelloToMs = R.partial(sayHello, ['Ms.']);
sayHelloToMs('Jane', 'Jones'); //=> 'Hello, Ms. Jane Jones!'
```

#### double
- `multiply2`는 인자로 받은 두 수를 곱한 결과를 반환하는 함수이다. `R.partial`에 함수 `multiply2`을 첫 번째 인자로 전달하고, 인자의 리스트가 담긴 배열인 `[2]`를 두 번째 인자로 전달하면, 인자의 리스트를 첫 번째 인자로 받은 함수 `multiply2`의 인자로 할당한다. 따라서 `multiply2(2)`가 되는 것이다. `multiply2` 함수는 2개의 인자를 받아야 하지만 하나의 인자를 받은 상태이며, 커링이 적용되지 않은 함수이지만 `R.partial`에 의해 마치 커링된 것 처럼 받은 인자를 머금고 있는 상태가 된다. 따라서 `double`이란 함수는 `multiply2(2)`으로 인자를 하나 더 받아 평가되는 함수이다. `double`은 `multiply2(2)(3)`이 되므로 결과는 6이 된다.

#### greet
- `greet` 함수는 인자를 문자열로 나열한다. `sayHello`는 `greet` 함수에 `'Hello'`란 인자를 미리 세팅한 함수이고, `sayHelloToMs`는 `sayHello`에 `'Ms.'`란 인자를 미리 세팅한 함수이고, `sayHelloToMs`란 함수는 `greet`라는 함수에 `salutation, title` 값이 미리 세팅이 되어 있는 것으로 `firstName, lastName`의 값만 받으면 되는 함수이다. 따라서 `sayHelloToMs('Jane', 'Jones')`으로 두 인자를 받아서 평가되어 `'Hello, Ms. Jane Jones!'`라는 결과를 반환한다.
