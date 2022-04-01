## anyPass
- `R.anyPass()`

## 설명
- R.any가 주어진 리스트의 원소들이 주어진 술어 함수를 모두 만족할 때 참이 되는 것과 달리, 주어진 술어 함수 리스트를 인자로 먼저 받고 주어진 값이 술어 함수 리스트를 모두 만족하는지 체크하여 참을 반환

## 표현
```
[(*… → Boolean)] → (*… → Boolean)
```
- `(*… → Boolean)` 리스트(예제에서는 객체)를 인자로 받아서 참, 거짓을 판별하는 술어함수
- `[(*… → Boolean)] →` 술어 함수가 들어 있는 리스트를 인자로 받는다.
- `[(*… → Boolean)] → (*… → Boolean)` 술어 함수가 들어 있는 리스트를 인자로 받아서 함수를 반환한다.
- `→ (*… → Boolean)` 반환된 함수는 리스트(예제에서는 객체)를 인자로 받아서 참 거짓을 판별한다.
- 곧 술어 함수가 들어 있는 리스트를 인자로 받아서 리스트에 속한 모든 술어 함수를 만족하는지 확인하여 참, 거짓을 판별한다.

## 예제
```
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


## Reference
- https://ramdajs.com/docs/#anyPass
