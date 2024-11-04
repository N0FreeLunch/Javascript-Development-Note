## anyPass

> Takes a list of predicates and returns a predicate that returns true for a given list of arguments if at least one of the provided predicates is satisfied by those arguments.
- 술어 함수의 리스트(술어함수를 원소로 하는 리스트)를 (인자로) 받고 (반환된 함수의) 주어진 인자의 리스트가 (반환되기 전) 제공된 술어 함수에 의해 (전달 되었을 때) 술어 함수 중에서 적어도 하나를 만족하면 참을 반환하는 술어함수를 반환한다.

> The function returned is a curried function whose arity matches that of the highest-arity predicate.
- 이 함수는 커링된 함수를 반환한다. 함수의 인자의 갯수는 가장 인자수가 많은 술어함수의 인자수와 일치한다.

> See also [allPass](./allPass.md), [either](./either.md).

### 설명
- 동일한 인자 세트를 여러 술어 함수에 전달 했을 때, 술어 함수들 중 적어도 하나를 만족하면 참을 반환하는 함수이다.
- R.any가 주어진 리스트의 원소들 중 어느 하나라도 주어진 술어 함수를 만족할 때 참이 되는 것과 달리, 주어진 술어 함수 리스트를 인자로 먼저 받고 인자 세트를 각각의 술어함수에 전달 했을 때 적어도 하나의 술어 함수를 만족하는지 확인하는 함수이다. R.any가 인자 리스트에서 어느 하나의 조건 만족을 판별한다면, R.anyPass는 고정된 인자 세트를 동일하게 술어함수에 전달 했을 때 어느 하나의 술어 함수를 만족하는지를 판별한다.
- R.allPass가 인자 세트를 술어함수 리스트에 전달 했을 때, 주어진 모든 술어 함수를 만족하면 true를 반환하는 것과 달리, R.anyPass는 인자 세트가 술어함수 리스트에 전달 되었을 때, 주어진 술어 함수 중 적어도 하나를 만족하면 true를 반환한다는 차이가 있다.

### 문법
```
R.anyPass(predicates): function
```

> `predicates`: An array of predicates to check
- `predicates`: (인자를 전달했을 때 참, 거짓을) 확인할 술어함수의 배열
> Returns function The combined predicate
- 함수를 반환한다. 이 함수는 술어 함수의 조합(combined)이다.

### 표현
```
[(*… → Boolean)] → (*… → Boolean)
```
- `[(*… → Boolean)] →` 술어 함수가 들어 있는 리스트를 인자로 받는다. - `(*… → Boolean)` 리스트(예제에서는 객체)를 인자로 받아서 참, 거짓을 판별하는 술어함수이다.
- `→ (*… → Boolean)`: 반환된 함수로 술어함수를 반환한다. 첫 번째 받은 배열의 원소인 술어함수와 인자에 동일한 구성의 `*…`인자를 전달한다. 술어 함수가 들어 있는 리스트를 인자로 받아서 리스트에 속한 적어도 하나의 술어 함수를 만족하는지 확인하여 참, 거짓을 판별한다.

### 예제
```js
const isClub = R.propEq('suit', '♣');
const isSpade = R.propEq('suit', '♠');
const isBlackCard = R.anyPass([isClub, isSpade]);

isBlackCard({rank: '10', suit: '♣'}); //=> true
isBlackCard({rank: 'Q', suit: '♠'}); //=> true
isBlackCard({rank: 'Q', suit: '♦'}); //=> false
```
- `R.propEq('suit', '♣')` 는 오브젝트의 프로퍼티 중에서 `suit` 키에 해당하는 값이 `'♣'`인지 확인하는 함수이다.
- `R.propEq('suit', '♠')` 는 오브젝트의 프로퍼티 중에서 `suit` 키에 해당하는 값이 `'♠'`인지 확인하는 함수이다.
- suit 값이 클로버인지 스페이드인지를 확인하는 방법은 `R.anyPass([isClub, isSpade])`로 만든 함수이다. 이 함수는 받을 리스트가 배열 안에 들어 있는 `isClub` `isSpade` 술어 함수를 모두 만족하는지 확인하는 함수 `isBlackCard`를 받환 한다.
- `isBlackCard`에 리스트 예를 들어 `{rank: '10', suit: '♣'}`나 `{rank: 'Q', suit: '♠'}`나 `{rank: 'Q', suit: '♦'}`를 넣었을 때 앞서 `isBlackCard`를 정의할 때 사용한 `isClub` `isSpade` 술어함수를 만족하는지 확인하는 것.
- 곧, `{rank: '10', suit: '♣'}`나 `{rank: 'Q', suit: '♠'}`나 `{rank: 'Q', suit: '♦'}` 안의 `suit` 프로퍼티의 값이 `isClub`이면 클로버인지 확인하고 `isSpade`이면 스페이스인지 확인을 하여 둘을 모두 만족하면 `isBlackCard(리스트)`에 의해서 참이 반환된다.

## References
- https://ramdajs.com/docs/#anyPass
- https://github.com/ramda/ramda/blob/master/test/anyPass.js
- https://github.com/ramda/types/blob/develop/types/anyPass.d.ts
