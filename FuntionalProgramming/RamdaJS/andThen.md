## andThen
- R.andThen()

## 설명
- 자바스크립트에서 promise 문법을 사용하면, promise로 비동기 요청을 했을 때, 요청의 값을 받아오는 시점에서 dot(.)으로 연결된 .then() 함수가 실행이 된다.
- 자바스크립트 promise 문법의 then을 함수형 표현으로 만든 것이 `R.andThen()` 함수이다.

## 표현
```
(a → b) → (Promise e a) → (Promise e b)
(a → (Promise e b)) → (Promise e a) → (Promise e b)
```

## 예제
```
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
- `R.andThen(R.pick(['firstName', 'lastName']))` promise의 결과 받는다.

## Reference
- https://ramdajs.com/docs/#andThen
