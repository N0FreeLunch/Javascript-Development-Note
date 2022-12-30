## allPass
> Takes a list of predicates and returns a predicate that returns true for a given list of arguments if every one of the provided predicates is satisfied by those arguments.

> The function returned is a curried function whose arity matches that of the highest-arity predicate.

> See also anyPass.

## 설명
- R.all이 하나의 술어 함수를 받아서 리스트에 들어있는 모든 원소가 술어함수를 만족하는지를 판별했다면, R.allPass는 복수의 술어 함수를 받아서 인자로 받은 대상이 복수개의 술어 함수 모두를 만족하는지 판별하는 함수이다.

## 문법
```
(allPass([predicates1, predicates2, predicates3, ...)])(literalObject)
```
반환값 `Boolean`

## 표현
```
[(*… → Boolean)] → (*… → Boolean)
```
- `(*… → Boolean)`에서 `*…`는 배열이든 오브젝트이든 어느 값이 되었든 단일 또는 여러 개의 인자를 받아서 참, 거짓을 판단하는, Boolean을 리턴하는 함수이다.
- `[(*… → Boolean)]` R.allPass는 참, 거짓을 판별하는 함수를 배열로 여러개 받을 수 있으며
- `→ (*… → Boolean)` R.allPass는 위에서 참 거짓을 판별하는 함수와 동일 타입의 인자를 넣었을 때 참, 거짓을 판별하는 함수를 반환한다. 여기서 동일 타입의 인자란 `[(*… → Boolean)]`에서 `(*… → Boolean)` 부분을 만들 때도 `*…` 기호를 썼듯이 ` → (*… → Boolean)` 에서도 동일한 타입의 `*…`를 인자로 받아야 하는 것을 의미한다.
- `[(*… → Boolean)] → (*… → Boolean)`는 참, 거짓을 판별하는 함수를 반환하는 것이며, R.allPass의 첫 번째 인자로는 `*…` 타입을 판별하는 함수를 단수 또는 복수개로 받는 배열을 인자로 하며, 두 번째 인자는 `*…` 타입의 인자를 받아서 첫 번째 인자로 받은 `*…` 타입의 값을 판별하는 함수들을 모두 만족하는지 판별하는 함수를 반환한다. 이 함수가 `→ (*… → Boolean)`에서 `(*… → Boolean)` 부분

## 예제
```
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

## Reference
- https://ramdajs.com/docs/#allPass
