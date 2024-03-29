## ifElse
> Creates a function that will process either the onTrue or the onFalse function depending upon the result of the condition predicate.

## 표현
```
(*… → Boolean) → (*… → *) → (*… → *) → (*… → *)
```
- `(*… → Boolean) →` 첫 번째 인자로 인자를 하나 또는 여러 개 받아 참 거짓을 반환하는 술어함수를 받는다.
- `→ (*… → *) →` 두 번째 인자로 술어함수가 참으로 평가될 때 실행할 함수를 받는다. 이 때 술어함수가 받는 인자와 동일한 인자를 받는다.
- `→ (*… → *) →` 세 번째 인자로 술어함수가 거짓으로 평가될 때 실행할 함수를 받는다. 이 때 술어함수가 받는 인자와 동일한 인자를 받는다.
- `→ (*… → *)` 반환된 함수는 첫 번째에서 세 번째 인자로 할당된 함수의 인자에 전달하기 위한 인자를 받고 술어 함수가 평가될 수 있는 양의 인자를 받으면 술어함수의 참 거짓이 판별되고 참 거짓에 따라 참이면 두 번째 인자로 주어진 함수에 인자를 전달하여 평가한 결과를 반환하고 거짓이면 세 번째 인자로 주어진 함수에 인자를 전달하여 평가한 결과를 반환한다.

## 설명
```
R.ifElse(술어함수, 술어함수가 참일 때 실행할 함수, 술어함수가 거짓일 때 실행할 함수)
```
- 첫 번째 인자로 술어함수를 받는다.
- 두 번째 인자로 술어함수가 참으로 평가될 때 실행할 함수를 받는다.
- 세 번째 인자로 술어함수가 거짓으로 평가될 때 실행할 함수를 받는다.
- 네 번째 인자 부터는 첫 번째 부터 세 번째 인자로 받은 함수가 실행될 때 받을 인자를 받는다. 이들 함수가 평가되기 위해 필요한 인자를 받게 되면 술어함수가 평가되고 술어함수의 참 거짓에 따라 참이면 두 번째 함수에 네 번째 인자 부터 받은 인자를 전달하여 실행한 결과를 반환하고 거짓이면 마찬가지로 인자를 전달하여 세 번째 함수에 인자들을 전달하여 실행한 결과를 반환한다.

## 예제
```
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

## Reference
- https://ramdajs.com/docs/#ifElse
