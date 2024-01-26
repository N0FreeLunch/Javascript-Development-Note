## otherwise
> Returns the result of applying the onFailure function to the value inside a failed promise. This is useful for handling rejected promises inside function compositions.
> 실패한 promise 내부 값에 onFailure 함수를(실패했을 때 실행되는 이밴트 함수) 적용할 결과를 반환한다. 이것은 함수의 조합(compositions)을 사용하여 거부된(rejected) promises를 헨들링하는데 유용하다.

> See also andThen.

### 설명

### 표현
```
(e → b) → (Promise e a) → (Promise e b)
(e → (Promise f b)) → (Promise e a) → (Promise f b)
```

###　예제
```js
const failedFetch = id => Promise.reject('bad ID');
const useDefault = () => ({ firstName: 'Bob', lastName: 'Loblaw' });

//recoverFromFailure :: String -> Promise ({ firstName, lastName })
const recoverFromFailure = R.pipe(
  failedFetch,
  R.otherwise(useDefault),
  R.andThen(R.pick(['firstName', 'lastName'])),
);
recoverFromFailure(12345).then(console.log);
```
- `recoverFromFailure(12345).then(console.log)`에서 `id` 값을 12345로 받아서 파이프가 실행된다.
- `R.pipe`는 인자로 나열된 함수를 순차적으로 실행하고 각 인자의 실행 결과를 다음 인자의 인자로 넣고 평가하는 함수이다. 따라서 함수의 적용 순서는 `failedFetch()`의 결과를 `R.otherwise(useDefault)(결과)`에 넣어주어 평가하고 평가된 결과를 ` R.andThen(R.pick(['firstName', 'lastName']))(결과)`에 넣어주어 함수를 평가한다. 
- `failedFetch` 함수는 `id`를 인자로 받아서 거부된(rejected) 프로미스(`Promise.reject('bad ID')`)를 반환하는 함수이다.
- `R.otherwise`는 실패 했을 때 실행할 함수를 첫 번째 인자로 받고, 두 번째 인자로 프로미스를 받는다. `R.pipe`에 의한 함수의 실행 결과로 실패한 프로미스를 받게 된다. 따라서 첫 번째 인자로 받은 실패했을 때 실행할 이벤트 함수를 실행하게 된다. `useDefault` 함수의 실행 결과로 `{ firstName: 'Bob', lastName: 'Loblaw' }`라는 결과 값을 얻는다.
- `R.andThen`은 프로미스 함수를 받았을 때 `.then(callbackFn)`을 ramda의 함수로 표현한 것이다. 콜백함수(callbackFn)는 `R.pick(['firstName', 'lastName'])`이다. `R.pick` 함수는 첫 번째 인자로 오브젝트에서 선택할 키를 배열로 받고, 두 번째 인자로 오브젝트를 받아서 선택할 키에 해당하는 키-벨류 쌍을 오브젝트로 반환하는 함수이다. 여기서는 `{ firstName: 'Bob', lastName: 'Loblaw' }`라는 결과가 파이프 함수의 실행에 의해 전달되었고, `callbackFn`의 인자로 `{ firstName: 'Bob', lastName: 'Loblaw' }`란 값을 전달한다. 선택되지 않은 키 없이 모든 키가 선택되어 반환된다. 따라서 `{ firstName: 'Bob', lastName: 'Loblaw' }` 프로미스의 결과로 넘긴다.
- 프로미스의 결과로 넘어왔기 때문에 `.then(console.log);`에서 해당 결과를 받아서 `{ firstName: 'Bob', lastName: 'Loblaw' }`란 결과를 출력한다. 

## Reference
- https://ramdajs.com/docs/#otherwise
