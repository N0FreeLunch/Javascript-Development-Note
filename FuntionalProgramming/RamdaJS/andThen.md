## andThen
> Returns the result of applying the onSuccess function to the value inside a successfully resolved promise. This is useful for working with promises inside function compositions.
- 프로미스가 성공적으로 리졸브(resolved) 되었을 때, 프로미스 내부의 값으로 성공했을 때 실행하는 이벤트 함수 `onSuccess`를 적용한 결과를 반환한다. `andThen` 함수는 함수의 컴포지션에서 프로미스를 조합하여 동작시킬 때 유용하다.

> See also [otherwise](./otherwise.md).

### 설명
- 자바스크립트에서 promise 문법을 사용하면, promise로 비동기 요청을 했을 때, 요청의 값을 받아오는 시점에서 dot(.)으로 연결된 .then() 함수가 실행이 된다.
- 자바스크립트 promise 문법의 then을 함수형 표현으로 만든 것이 `R.andThen()` 함수이다.

### 표현
```
(a → b) → (Promise e a) → (Promise e b)
(a → (Promise e b)) → (Promise e a) → (Promise e b)
```
- `(a → b) →` 첫 번째 인자로 성공했을 때 실행할 이벤트 함수를 받는다.
- `→ (Promise e a) →` 두 번째 인자로 프로미스를 받는다.
- `→ (Promise e b)` 프로미스를 반환한다. 이때 두 번째 인자에서 프로미스가 받는 값을 `a`라고 했을 때 반환된 프로미스는 첫 번째 인자의 함수에 `a`를 전달한 결과값인 `b`를 받는다.

### 예제
```js
const makeQuery = email => ({ query: { email }});
const fetchMember = request =>
  Promise.resolve({ firstName: 'Bob', lastName: 'Loblaw', id: 42 });

//getMemberName :: String -> Promise ({ firstName, lastName })
const getMemberName = R.pipe(
  makeQuery,
  fetchMember,
  R.andThen(R.pick(['firstName', 'lastName']))
);

getMemberName('bob@gmail.com').then(console.log);
```
- `makeQuery`는 `email` 값을 넣었을 때, `{ query: { email }}`라는 오브젝트를 반환하는 함수이다.
- `fetchMember`는 인자를 받았을 때 결과 값을 promise로 평가해서 반환하는 함수이다.
- `R.andThen(R.pick(['firstName', 'lastName']))`은 인자로 `R.pick(['firstName', 'lastName']`을 넣었을 때 `makeQuery` 함수와 `fetchMember` 함수를 합성하여 머금고 있는 함수이며 promise의 결과 받는다. `makeQuery`와 `fetchMember`를 합성한 함수에 `R.pick(['firstName', 'lastName'])`인자를 전달하고 결과 값을 promise의 평가 값으로 받는 함수가 여기서의 `R.andThen` 함수
- R.pipe 함수에 의해서 `makeQuery` 함수는 `fetchMember` 함수의 인자로 들어가 합성 함수를 만들고 `makeQuery`와 `fetchMember`의 합성 함수가 `R.andThen(R.pick(['firstName', 'lastName']))`로 만들어진 함수의 인자로 들어가 합성 함수를 만든다. 이렇게 만들어진 함수가 `getMemberName`
- `getMemberName('bob@gmail.com')` `getMemberName` 함수에 `'bob@gmail.com'` 메일 주소를 넣으면 내부에서 promise로 평가하는 과정을 거쳐서 promise 타입의 반환 값이 된다. promise 타입의 반환 값을 사용하기 위해서는 `.then(console.log)` then 문법을 사용해서 콜백으로 전달되는 값을 받으면 된다.

## Reference
- https://ramdajs.com/docs/#andThen
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
