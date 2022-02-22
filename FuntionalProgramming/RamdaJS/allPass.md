## allPass
- R.allPass()

## 설명


## 표현
```
[(*… → Boolean)] → (*… → Boolean)
```
- `(*… → Boolean)` 리터럴 오브젝트를 판별하는 함수
- `[(*… → Boolean)]` 리터럴 오브젝트를 판별하는 함수를 배열 로 여러개 받을 수 있으며
- `(*… → Boolean)` 리터럴 오브젝트를 넣었을 때 참, 거짓을 판별하는 함수를 반환한다.
- `[(*… → Boolean)] → (*… → Boolean)`는 참, 거짓을 판별하는 함수를 반환하는 것이며, R.allPass의 첫 번째 인자로는 오브젝트를 판별하는 함수를 단수 또는 복수개로 받는 배열을 인자로 하며, 두 번째 인자는 리터럴 오브젝트를 받아서 첫 번째 인자로 받은 오브젝트 판별 함수 둘을 만족하는지 판별하는 함수를 반환한다. 그것이 `→ (*… → Boolean)`에서 `(*… → Boolean)` 부분


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
- `isQueenOfSpades({rank: 'Q', suit: '♣︎'}); //=> false` 주어진 오브젝트 `{rank: 'Q', suit: '♣︎'`가 배열 안에 든 두 개의 술어 함수 `[isQueen, isSpade]`를 만족하는지 확인
- `isQueenOfSpades({rank: 'Q', suit: '♠︎'}); //=> true` 주어진 오브젝트 `{rank: 'Q', suit: '♠︎'}`가 배열 안에 든 두 개의 술어 함수 `[isQueen, isSpade]`를 만족하는지 확인

## Reference
- https://ramdajs.com/docs/#allPass
