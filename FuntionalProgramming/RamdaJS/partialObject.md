## partialObject

> Takes a function f and an object, and returns a function g. When applied, g returns the result of applying f to the object provided initially merged deeply (right) with the object provided as an argument to g.
- 함수 f와 하나의 오브젝트를 받아서 함수 g를 반환한다. partialObject 함수에 f와 오브젝트가 적용된 함수 g는 주어진 초기 오브젝트가 함수 f에 적용한 결과 함수 g를 반환한다. 함수 g는 인자로 주어진 오브젝트가 g로 (오른쪽으로) 깊은 병합(merged deeply)된 것이다.

> See also partial, partialRight, curry, mergeDeepRight.

### 설명

### 표현
```
(({ a, b, c, …, n }) → x) → { a, b, c, …} → ({ d, e, f, …, n } → x)
```
- `(({ a, b, c, …, n }) → x) →`는 하나의 오브젝트를 받고, 이 오브젝트는 n개의 키인 `({ a, b, c, …, n })`로 a, b, c ... n을 받아 결과 x를 반환하는 함수를 받는다.
- `→ { a, b, c, …} → `는 첫 번째 인자로 받은 함수의 인자로 받는 오브젝트의 키의 갯수 n개 까지가 아닌 일부 `{ a, b, c, …}` 키를 갖는 오브젝트를 받는다.
- `→ ({ d, e, f, …, n } → x)`는 하나의 오브젝트에 이미 받지 못한 나머지 키를 갖는 오브젝트인 `{ d, e, f, …, n }`를 받아서 첫 번째 인자로 받은 함수의 결과값에 해당하는 x를 반환한다.

### 예제
```js
onst multiply2 = ({ a, b }) => a * b;
const double = R.partialObject(multiply2, { a: 2 });
double({ b: 2 }); //=> 4

const greet = ({ salutation, title, firstName, lastName }) =>
  salutation + ', ' + title + ' ' + firstName + ' ' + lastName + '!';

const sayHello = R.partialObject(greet, { salutation: 'Hello' });
const sayHelloToMs = R.partialObject(sayHello, { title: 'Ms.' });
sayHelloToMs({ firstName: 'Jane', lastName: 'Jones' }); //=> 'Hello, Ms. Jane Jones!'
```

#### double
- `multiply2`는 하나의 인자를 받는다. 이 때 하나의 인자는 오브잭트로 이 오브젝트는 키 a와 키 b를 가지고 있다. 이 함수는 오브젝트의 키 a, b를 받아서 이를 곱하는 연산을 한 결과를 반환한다.
- `R.partialObject(multiply2, { a: 2 })`는 오브젝트의 키값을 서로 곱하는 함수의 인자 a, b를 모두 받지 않고, 하나만을 가진 상태의 함수를 만들어 반환한다.
- 반환된 함수 `double`는 나머지 인자 b를 오브젝트의 키로 받아 `{ b: 2 }`, `multiply2`의 연산에 필요한 오브젝트의 모든 키를 받는다.

#### greet
- `greet`는 하나의 오브젝트를 받으며 이 오브젝트는 `salutation`, `title`, `firstName`, `lastName`로 4개의 키를 받는다.
- `R.partialObject(greet, { salutation: 'Hello' })`코드를 보면 `salutation`이란 키 하나를 이미 하나 받은 형태의 `greet` 함수인 `sayHello`를 만들고, `title`이란 키 하나를 이미 하나 받은 형태의 `sayHello` 함수인 `sayHelloToMs`를 만든다. `sayHelloToMs` 함수는 `salutation` 키와 `title`키 값을 이미 가진 형태의 함수이기 때문에 `greet`가 받는 오브젝트의 4개의 키 중에서 나머지 2개만을 더 받으면 평가 될 수 있다. 따라섯 `sayHelloToMs({ firstName: 'Jane', lastName: 'Jones' })`으로 키를 두 개 더 받아 결과값을 반환한다.

## Reference
- https://ramdajs.com/docs/#partialObject
