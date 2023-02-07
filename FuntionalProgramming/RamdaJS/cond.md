## cond
> Returns a function, fn, which encapsulates if/else, if/else, ... logic. R.cond takes a list of [predicate, transformer] pairs.
- if/else 로직을 캡슐화하는 함수를 반환한다. `R.cond`는 술어함수와 변환함수의 쌍 `[술어함수, 변환함수]`을 원소로 하는 리스트를 받는다.
> All of the arguments to fn are applied to each of the predicates in turn until one returns a "truthy" value, at which point fn returns the result of applying its arguments to the corresponding transformer.
- (이때, 함수 `fn`은 `R.cond([[predicate, transformer]...])`을 의미하며 이 함수는 인자를 하나 받아 평가되는 함수이다.)
- fn에 적용되는 모든 인자는 술어 함수가 참인 값을 반환할 때까지 주어진 `[술어함수, 변환함수]` 리스트의 술어함수의 인자로 전달된다. 전달된 인자로 술어함수가 평가되어 참인 값을 반환하면 `fn`은 `[술어함수, 변환함수]`의 리스트를 순회하면서 술어함수에 전달했던 인자를 참을 반환했던 술어함수와 쌍을 이루는 변환함수에 적용한 결과를 반환한다.
> If none of the predicates matches, fn returns undefined.
- 만약 인자를 술어함수의 인자로 전달해서 참인 값이 나오는 대상이 `[술어함수, 변환함수]`의 리스트에 존재하지 않으면 `fn`함수는 `undefined`를 반환한다.
> Please note: This is not a direct substitute for a switch statement. Remember that both elements of every pair passed to cond are functions, and cond returns a function.
- 참고 : `cond` 함수는 `switch`문을 직접적으로 대체하지 않는다. `cond`함수로 전달되는 모든 `[술어함수, 변환함수]`의 쌍은 함수라는 것과 `cond`는 함수(fn)을 반환한다는 것을 기억하라.

> See also ifElse, unless, when.

## 설명

## 표현
```
[[(*… → Boolean),(*… → *)]] → (*… → *)
```

## 예제
```
const fn = R.cond([
  [R.equals(0),   R.always('water freezes at 0°C')],
  [R.equals(100), R.always('water boils at 100°C')],
  [R.T,           temp => 'nothing special happens at ' + temp + '°C']
]);
fn(0); //=> 'water freezes at 0°C'
fn(50); //=> 'nothing special happens at 50°C'
fn(100); //=> 'water boils at 100°C'
```
- `R.cond([[술어함수, 변환함수]...])`의 형태에서 리스트의 각각의 원소는 `[술어함수, 변환함수]`의 쌍으로 구성된다.
- `[R.equals(0),   R.always('water freezes at 0°C')]`에서 술어함수는 `R.equals(0)`이며 인자를 하나 받아서 해당 값이 `0`인지 판단하는 함수이다. 변환함수는 `R.always('water freezes at 0°C')`에 해당한다. 만약 인자를 하나 받아서 평가된 값이 참이라면 변환함수를 실행하고 실행한 결과를 반환하고 참이 아니라면 변환함수를 실행하지 않는다. 이 때 변환함수도 마찬가지로 같은 인자를 받아서 `변환함수(0)`으로 실행이 되고 이 값이 반환되지만 `R.always()`이므로 두 번째 인자가 무엇이 오든 첫 번째로 할당한 인자 값이 반환된다.
- `[R.equals(100), R.always('water boils at 100°C')]`에서 술어함수는 `R.equals(100)`이고 변환함수는 `R.always('water boils at 100°C')`에 해당한다. 만약 인자를 하나 전달 받아서 그 값이 100이라면 술어함수는 참을 반환한다. 술어함수가 참을 반환하면 주어진 변환 함수가 `변환함수(100)` 꼴로 실행되어 그 결과 값이 반환되는데 `R.always()`이므로 두 번째 인자가 무엇이 오든 첫 번째로 할당한 인자 값이 반환된다.
- `[R.T,           temp => 'nothing special happens at ' + temp + '°C']`에서 술어함수는 `R.T`이고 변환함수는 `temp => 'nothing special happens at ' + temp + '°C'`에 해당한다. 술어함수 `R.T`는 어떤 인자를 받든지 항상 참을 반환하는 함수이다. `[술어함수, 변환함수]`의 쌍의 리스트에서 리스트의 앞선 인덱스의 술어함수가 먼저 실행된다. 먼저 매칭되는 술어함수가 없을 경우 마지막으로 어느 인자를 받든지 항상 참을 반환하는 함수를 받아서 최소한 `R.T`에 매칭되는 변환함수는 실행하여 반환하려는 의도를 가지고 있다. 이 때 변환함수가 평가될 때는 `(temp => 'nothing special happens at ' + temp + '°C')(R.T 술어함수에 전달받은 인자)`가 들어가게 된다.
- 최종적으로는 `[술어함수, 변환함수]`를 세트로 하는 리스트의 술어함수를 만족하는 대상의 변환함수를 실행한 결과를 반환한다. 만약 매칭되는 술어함수가 존재하지 않는다면, `undefined`를 반환한다.
- `fn(0)`은 첫 번째 술어함수에 매칭되어 첫 번째 변환함수를 실행한 결과값을 갖는다.
- `fn(50)`은 세 번째 술어함수에 매칭되어 세 번째 변환함수를 실행한 결과값을 갖는다.
- `fn(100)`은 두 번째 술어함수에 매칭되며 두 번째 변환함수를 실행한 결과값을 갖는다. 이 때 변환함수는 `(temp => 'nothing special happens at ' + temp + '°C')(100)`를 실행하고 fn의 실행 결과로 반환한다.

## Reference
- https://ramdajs.com/docs/#cond
