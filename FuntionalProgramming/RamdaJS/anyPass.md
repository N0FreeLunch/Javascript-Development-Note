
## 설명
- R.any가 주어진 리스트의 원소들이 주어진 술어 함수를 모두 만족할 때 참이 되는 것과 달리, 주어진 술어 함수 리스트를 인자로 먼저 받고 주어진 값이 술어 함수 리스트를 모두 만족하는지 체크하여 참을 반환

## 표현
```
(a → Boolean) → [a] → Boolean
```
- `(a → Boolean)` 술어 함수를 인자로 받는다.



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
- suit 값이 클로버인지 스페이드인지를 확인하는 방법은 


## Reference
- https://ramdajs.com/docs/#anyPass
