## allPass

> Takes a list of predicates and returns a predicate that returns true for a given list of arguments if every one of the provided predicates is satisfied by those arguments.
- 술어함수의 (술어함수를 원소로 하는) 리스트를 (인자로) 받아 술어함수를 반환한다. 반환된 함수는 주어진 인자의 리스트에 대해 제공된 술어함수를 모두 만족한다면 (인자를 제공된 술어함수에 전달해서 평가된 경과가 모두 참이되면) true를 반환한다.

> The function returned is a curried function whose arity matches that of the highest-arity predicate.
- 이 함수는 커링된 함수를 반환하는데, 반환된 이 함수의 (평가를 위하 필요한) 인자의 수는 (반환 전의 술어함수 리스트에서) 인자의 수가 가장 높은 술어함수의 인자수와 일치한다.

> See also [anyPass](./anyPass.md).

### 설명
- R.all이 하나의 술어 함수를 받아서 리스트에 들어있는 모든 원소가 술어함수를 만족하는지를 판별했다면, R.allPass는 복수의 술어 함수를 받아서 인자로 받은 대상이 복수개의 술어 함수 모두를 만족하는지 판별하는 함수이다.

### 문법

```
R.allPass(predicates: predicate[]): function
```
- `predicates`: An array of predicates to check
- Returns function The combined predicate

### 표현

```
[(*… → Boolean)] → (*… → Boolean)
```
- `[(*… → Boolean)]`: R.allPass는 참, 거짓을 판별하는 술어 함수를 배열로 여러개 받을 수 있다는 의미를 가진다. 배열 부분을 제하고 생각하면 `(*… → Boolean)`에서 `*…`는 배열이든 오브젝트이든 단일 또는 여러 개의 인자를 인자의 수나 종류의 제한없이 받아서 참, 거짓을 판단하는, Boolean을 리턴하는 술어함수라는 것을 알 수 있다.
- `→ (*… → Boolean)`: R.allPass의 반환 함수는 술어함수인데, R.allPass에 전달한 술어함수의 리스트의 각 술어함수에 전달할 인자의 타입과 수와 일치하는 인자의 타입과 수를 받아야 한다. 여기서 동일 타입의 인자란 술어함수 리스트 `[(*… → Boolean)]`에서 각각의 술어함수의 `(*… → Boolean)` 시그니처에서 `*…` 기호를 썼듯이, 반환된 함수의 시그니처 `→ (*… → Boolean)`에서도 동일한 타입의 `*…`를 인자로 받아야 하는 것을 의미한다.

### 예제

```js
const isQueen = R.propEq('rank', 'Q');
const isSpade = R.propEq('suit', '♠︎');
const isQueenOfSpades = R.allPass([isQueen, isSpade]);

isQueenOfSpades({rank: 'Q', suit: '♣︎'}); //=> false
isQueenOfSpades({rank: 'Q', suit: '♠︎'}); //=> true
```
- `const isQueen = R.propEq('rank', 'Q')`는 오브젝트가 가진 `rank` 키 값이 `'Q'`인지 확인하고 참, 거짓을 반환하는 함수
- `const isSpade = R.propEq('suit', '♠︎')`도 마찬가지로 오브젝트가 가진 `suit` 키 값이 `'♠︎'`인지 확인하고 참, 거짓을 반환하는 함수
- `const isQueenOfSpades = R.allPass([isQueen, isSpade]);` 주어진 오브젝트가 배열에 담긴 술어함수를 모두 만족하는지를 확인하는 함수를 만듦
- `isQueenOfSpades({rank: 'Q', suit: '♣︎'}); //=> false` 주어진 오브젝트 `{rank: 'Q', suit: '♣︎'}`가 배열 안에 든 두 개의 술어 함수 `[isQueen, isSpade]`를 만족하는지 확인
- `isQueenOfSpades({rank: 'Q', suit: '♠︎'}); //=> true` 주어진 오브젝트 `{rank: 'Q', suit: '♠︎'}`가 배열 안에 든 두 개의 술어 함수 `[isQueen, isSpade]`를 만족하는지 확인

## References
- https://ramdajs.com/docs/#allPass
- https://github.com/ramda/ramda/blob/master/test/allPass.js
- https://github.com/ramda/types/blob/develop/types/allPass.d.ts
