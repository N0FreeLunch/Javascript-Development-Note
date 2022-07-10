## both
- R.both
> A function which calls the two provided functions and returns the && of the results.
- 
> It returns the result of the first function if it is false-y and the result of the second function otherwise.
- 
> Note that this is short-circuited, meaning that the second function will not be invoked if the first returns a false-y value.
- 
> In addition to functions, R.both also accepts any fantasy-land compatible applicative functor.
- 


## 표현
```
(*… → Boolean) → (*… → Boolean) → (*… → Boolean)
```


## 설명
- `R.both` 함수는 두 개의 술어함수를 받는다.
- 두 개의 술어함수를 받고 반환된 함수는 하나의 인자를 받는데 미리 받은 두 개의 술어함수에 인자로 할당했을 때 둘 중 하나라도 거짓이라면 거짓을 둘 다 참이라면 참은 반환하는 함수이다.


## 예제
```
const gt10 = R.gt(R.__, 10)
const lt20 = R.lt(R.__, 20)
const f = R.both(gt10, lt20);
f(15); //=> true
f(30); //=> false

R.both(Maybe.Just(false), Maybe.Just(55)); // => Maybe.Just(false)
R.both([false, false, 'a'], [11]); //=> [false, false, 11]
```
- `R.gt(R.__, 10)`에서 `R.__`는 미리 받아야 할 인자를 나중에 받을 수 있도록 하는 기능. `gt10`함수에는 `R.__` 부분에 해당하는 인자를 받게 된다. 곧, 받은 인자가 10보다 큰지 체크하여 참, 거짓을 반환하는 함수이다.
- `R.lt(R.__, 20)`으로 만들어진 `lt20`함수는 인자로 `R.__` 부분에 해당하는 인자 값을 받는다. 곧, 받은 인자가 20보다 작은지를 체크하여 참, 거짓을 반환하는 함수이다.
- `R.both`는 인자롤 받은 두 술어함수에 동일한 인자를 넣어 두 술어함수를 만족하면 참, 하나라도 거짓이거나 모두 거짓인 경우 거짓을 반환하는 함수가 된다.
- `R.both(gt10, lt20)`으로 만들어진 f는 10보다 크고 20보다 작은지를 체크하는 술어함수가 된다.
- `f(15);`에서 15는 10보다 크고 20보다 작으므로 참을 반환한다.
- `f(30);`애서 30은 10보타 크다는 것은 참이지만 20보다 크다는 것은 거짓이므로 거짓을 반환한다.


## Reference
- https://ramdajs.com/docs/#both
