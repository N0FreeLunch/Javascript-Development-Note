## cond
> Returns a function, fn, which encapsulates if/else, if/else, ... logic. R.cond takes a list of [predicate, transformer] pairs.
- if/else 로직을 캡슐화하는 함수를 반환한다. `R.cond`는 술어함수와 변환함수의 쌍 `[술어함수, 변환함수]`을 원소로 하는 리스트를 받는다.
> All of the arguments to fn are applied to each of the predicates in turn until one returns a "truthy" value, at which point fn returns the result of applying its arguments to the corresponding transformer.
- fn에 대한 모든 인수는 참인 값을 반환할 때까지 각 술어에 차례로 적용됩니다. 이때 `fn`은 인수를 해당 변환함수에 적용한 결과를 반환합니다.
> If none of the predicates matches, fn returns undefined.
- 술어함수에 매칭되지 않으면 fn은 undefined를 반환한다.
> Please note: This is not a direct substitute for a switch statement. Remember that both elements of every pair passed to cond are functions, and cond returns a function.
- 참고 : `cond` 함수는 `switch`문을 직접적으로 대체하지 않는다. `cond`함수로 전달되는 모든 술어함수, 변환함수의 쌍은 함수라는 것과 `cond`는 함수를 반환한다는 것을 기억하라.

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
- `[R.equals(0),   R.always('water freezes at 0°C')]`에서 술어함수는 `R.equals(0)`이며 인자를 하나 받아서 해당 값이 `0`인지 판단하는 함수이다. 변환함수는 `R.always('water freezes at 0°C')`에 해당한다. 만약 인자를 하나 받아서 평가된 값이 참이라면 변환함수를 실행하고 실행한 결과를 반환하고 참이 아니라면 술어함수를 실행하지 않는다. 이 때 변환함수는 아무 인자도 받지 않고 `변환함수()`꼴로 함수가 실행된다.
- `[R.equals(100), R.always('water boils at 100°C')]`에서 술어함수는 `R.equals(100)`이고 변환함수는 `R.always('water boils at 100°C')`에 해당한다. 만약 인자를 하나 전달 받아서 그 값이 100이라면 술어함수는 참을 반환한다. 술어함수가 참을 반환하면 주어진 변환 함수가 `변환함수()` 꼴로 실행되고 술어함수가 참이 아니라면 변환 함수는 실행되지 않는다.
- `[R.T,           temp => 'nothing special happens at ' + temp + '°C']`에서 술어함수는 `R.T`이고 변환함수는 `temp => 'nothing special happens at ' + temp + '°C'`에 해당한다. 술어함수 `R.T`는 어떤 인자를 받든지 항상 참을 반환하는 함수이다.
- 최종적으로는 `[술어함수, 변환함수]`를 세트로 하는 리스트의 술어함수를 만족하는 대상의 변환함수를 실행한 결과를 반환한다. 만약 매칭되는 술어함수가 존재하지 않는다면, `undefined`를 반환한다.
- `fn(0)`은 첫 번째 술어함수에 매칭되어 첫 번째 변환함수를 실행한 결과값을 갖는다.
- `fn(50)`은 세 번째 술어함수에 매칭되어 세 번째 변환함수를 실행한 결과값을 갖는다.
- `fn(100)`은 두 번째 술어함수에 매칭되며 두 번째 변환함수를 실행한 결과값을 갖는다.

## Reference
- https://ramdajs.com/docs/#cond
