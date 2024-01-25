## once
> Accepts a function fn and returns a function that guards invocation of fn such that fn can only ever be called once, no matter how many times the returned function is invoked. The first value calculated is returned in subsequent invocations.
- 함수 fn을 인자로 받아서 fn 함수가 한 번만 호출될 수 있도록 fn 함수의 호출을 보호하는 함수를 반환한다. 반환된 함수가 몇 번 호출되든지 상관없이, 계산된 첫 번째 값은 후속 호출에서 반환된다.

> Open in REPLRun it here

### 설명
- 어떤 함수를 한 번만 호출하고 싶을 때 사용한다. 함수를 한 번 호출했을 때는 함수 내부의 로직이 실행되고, 후속 호출은 캐시된 값을 반환하며 내부 로직을 실행하지 않는다.
- 한 번만 호출하고 싶은 함수를 fn이라고 하자. 이 함수를 `once` 함수의 첫 번째 인자로 전달하면, 한 번만 호출되고 후속 호출은 캐시된 값을 반환하는 함수가 반환된다.
- once의 반환된 함수를 첫 번째 실행 할 때는, `fn`의 로직을 수행한 결과값을 반환한다.
- once의 반환된 함수를 두 번째 실행 할 때는, `fn`의 로직은 동작시키지 않고 첫 번째 실행 결과를 반환한다. 세 번째, 네 번째 ... 실행에서도 마찬가지로 첫 번째 실행 결과값을 반환한다.

### 표현
```
(a… → b) → (a… → b)
```
- `(a… → b) →` 첫 번째 인자로 함수를 받는다. `a…` 이 함수는 여러 종류의 인자를 여럿 받을 수 있다. 
- `→ (a… → b)` 반환 함수이며 이 함수에 어느 값을 넣든 첫 번째는 첫 번재 함수를 실행하고 후속 호출에는 첫 번째 호출과 동일한 결과값을 반환한다.

### 예제
```
const addOneOnce = R.once(x => x + 1);
addOneOnce(10); //=> 11
addOneOnce(addOneOnce(50)); //=> 11
```
- 함수 `x => x + 1`의 로직을 한 번만 실행되는 함수를 만들기 위해 `R.once` 함수의 인자로 전달하였다. 반환된 함수는 `addOneOnce`으로 이름을 지어 주었다.
- `addOneOnce(10);` 첫 번째 호출할 때는 `x => x + 1`의 로직이 실행되어 11의 값을 얻는다.
- 후속 호출에서는 `addOneOnce(addOneOnce(50))`으로 `addOneOnce` 함수를 두 번이나(세번째 네번째 호출) 사용했지만, 첫 번째 호출의 캐시값인 11을 반환할 뿐이다.

## Reference
- https://ramdajs.com/docs/#once
