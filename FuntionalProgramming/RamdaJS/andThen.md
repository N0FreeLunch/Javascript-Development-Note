## andThen
- R.andThen()

## 설명

## 표현

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

## Reference
- https://ramdajs.com/docs/#andThen
