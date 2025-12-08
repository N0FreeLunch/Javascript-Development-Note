# ifElse

> Creates a function that will process either the onTrue or the onFalse function depending upon the result of the condition predicate.
- 함수를 생성한다. 이 함수는 (조건이 참일 때 실행되는 함수) onTrue 또는 (조건이 거짓일 때 실행되는 함수) onFalse 함수 둘 중 하나를 처리하며 (언어의 if문의 상태 판단 위치의 값) 상태 술어의 결과에 의존(처리를 분기)한다.
> Note that ifElse takes its arity from the longest of the three functions passed to it.
- ifElse는 단항 함수를 받고 (상태 술어함수, 참일 때 실행하는 함수, 거짓일 때 실행하는 함수) 최대 3개의 함수를 전달할 수 있다.
> See also [unless](./unless.md), [when](./when.md), [cond](./cond.md).

## 설명

- if, else의 프로그래밍 언어의 구문에 의존하는 방식의 코딩이 아닌, 함수를 통해서 이 구문을 제어하는 방식을 사용한다. `R.ifElse`의 결과로 반환된 함수에 단항 인자를 전달할 때, 함수의 처리가 실행되기 때문에 지연평가의 로직을 형성할 때 적절하다.

```
R.ifElse(술어함수, 술어함수가 참일 때 실행할 함수, 술어함수가 거짓일 때 실행할 함수)
```

- 첫 번째 인자로 술어함수를 받는다.
- 두 번째 인자로 술어함수가 참으로 평가될 때 실행할 함수를 받는다.
- 세 번째 인자로 술어함수가 거짓으로 평가될 때 실행할 함수를 받는다.
- 네 번째 인자 부터는 첫 번째 부터 세 번째 인자로 받은 함수가 실행될 때 받을 인자를 받는다. 이들 함수가 평가되기 위해 필요한 인자를 받게 되면 술어함수가 평가되고 술어함수의 참 거짓에 따라 참이면 두 번째 함수에 네 번째 인자 부터 받은 인자를 전달하여 실행한 결과를 반환하고 거짓이면 마찬가지로 인자를 전달하여 세 번째 함수에 인자들을 전달하여 실행한 결과를 반환한다.

## 문법

```
R.ifElse(condition, onTrue, onFalse): function
```

> `condition`: A predicate function
- `condition`: 술어함수
> `onTrue`: A function to invoke when the condition evaluates to a truthy value.
- `onTrue`: 상태가 truthy 값으로 평가될 때 호출할 함수
> `onFalse`: A function to invoke when the condition evaluates to a falsy value.
- `onFalse`: 상태가 falsy 값으로 평가될 때 호출할 함수
> Returns function A new function that will process either the `onTrue` or the `onFalse` function depending upon the result of the `condition` predicate.
- 함수를 반환한다. (반환 값으로 생성된) 새로운 함수는 `onTrue` 또는 `onFalse` 함수 둘 중 하나를 처리하며, (둘 중 어느것을 선택할지는) `condition` 술어함수의 결과에 따른다.

## 표현

```
(*… → Boolean) → (*… → *) → (*… → *) → (*… → *)
```

- `(*… → Boolean) →`: 첫 번째 인자로 인자를 하나 또는 여러 개 받아 참 거짓을 반환하는 술어함수를 받는다.
- `→ (*… → *) →`: 두 번째 인자로 술어함수가 참으로 평가될 때 실행할 함수를 받는다. 이 때 술어함수가 받는 인자와 동일한 인자를 받는다.
- `→ (*… → *) →`: 세 번째 인자로 술어함수가 거짓으로 평가될 때 실행할 함수를 받는다. 이 때 술어함수가 받는 인자와 동일한 인자를 받는다.
- `→ (*… → *)`: 반환된 함수는 첫 번째에서 세 번째 인자로 할당된 함수의 인자에 전달하기 위한 인자를 받고 술어 함수가 평가될 수 있는 양의 인자를 받으면 술어함수의 참 거짓이 판별되고 참 거짓에 따라 참이면 두 번째 인자로 주어진 함수에 인자를 전달하여 평가한 결과를 반환하고 거짓이면 세 번째 인자로 주어진 함수에 인자를 전달하여 평가한 결과를 반환한다.

## 예제

```js
const incCount = R.ifElse(
  R.has('count'),
  R.over(R.lensProp('count'), R.inc),
  R.assoc('count', 1)
);
incCount({ count: 1 }); //=> { count: 2 }
incCount({});           //=> { count: 1 }
```
- 첫 번째 인자로 `R.has('count')`로 만들어진 함수는 오브젝트를 인자로 받아서 `count`라는 프로퍼티가 존재하는지 확인한다.
- 두 번째 인자로 `R.over(R.lensProp('count'), R.inc)`로 만들어진 함수는 오브젝트를 인자로 받아서 `count`라는 프로퍼티의 값을 가져와 1을 더한 값을 반환하는 함수이다.
- 세 번째 인자로 `R.assoc('count', 1)`로 만들어진 함수는 오브젝트를 인자로 받아서 새 오브젝트를 하나 생성하는데 `count` 프로퍼티가 1인 오브젝트를 생성하여 반환하는 함수이다.
- `incCount({ count: 1 })`는 술어함수에 `{ count: 1 }`를 전달하고 `count`라는 프로퍼티가 존재하므로 두 번째 함수에 `{ count: 1 }` 오브젝트를 전달하여 프로퍼티 값을 지정한 함수를 적용한 값으로 바꾼 결과를 반환하므로 `{ count: 2 }`가 된다.
- `incCount({}); `는 술어함수에 `{}`를 전달하고 `count`라는 프로퍼티가 없으므로 세 번째 함수에 `{}` 오브젝트를 전달하여 평가된 결과 `{ count: 1 }`를 반환한다.

## References

- https://ramdajs.com/docs/#ifElse
- https://github.com/ramda/ramda/blob/master/test/ifElse.js
- https://github.com/ramda/types/blob/develop/types/ifElse.d.ts
