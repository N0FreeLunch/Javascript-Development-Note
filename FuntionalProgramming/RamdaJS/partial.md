## partial
> Takes a function f and a list of arguments, and returns a function g. When applied, g returns the result of applying f to the arguments provided initially followed by the arguments provided to g.

### 설명

### 표현

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
- `multiply2`는 인자로 받은 두 수를 곱한 결과를 반환하는 함수이다. `R.partial`에 함수 `multiply2`을 첫 번째 인자로 전달하고, 인자의 리스트가 담긴 배열인 `[2]`를 두 번째 인자로 전달하면, 인자의 리스트를 첫 번째 인자로 받은 함수 `multiply2`의 인자로 할당한다. 따라서 `multiply2(2)`가 되는 것이다. `multiply2` 함수는 2개의 인자를 받아야 하지만 하나의 인자를 받은 상태이며, 커링이 적용되지 않은 함수이지만 `R.partial`에 의해 자동으로 커링이 되어 받은 하나의 인자를 머금고 있는 상태가 된다. 따라서 `double`이란 함수는 `multiply2(2)`으로 인자를 하나 더 받아 평가되는 함수이다. `double`은 `multiply2(2)(3)`이 되므로 결과는 6이 된다.

#### 
