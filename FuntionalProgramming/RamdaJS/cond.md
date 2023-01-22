## cond
> Returns a function, fn, which encapsulates if/else, if/else, ... logic. R.cond takes a list of [predicate, transformer] pairs.
- if/else 로직을 캡슐화하는 함수를 반환한다. `R.cond`는 술어함수와 변환함수의 쌍(`[술어함수, 변환함수]`)의 리스트를 받는다.
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

## Reference
- https://ramdajs.com/docs/#cond
