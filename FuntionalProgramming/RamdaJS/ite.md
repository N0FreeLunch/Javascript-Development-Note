## ite
> Returns true if the first argument is less than or equal to the second; false otherwise.
- 첫 번째 이자가 두 번째 인자보가 작거나 같으면 참을 반환하고 아니면 거짓을 반환한다.

## 설명
- `첫 번째 인자 <= 두 번째 인자`의 연산을 의미한다.

## 표현
```
Ord a => a → a → Boolean
```
- `Ord a =>` 순서가 있는 타입인 a에 대해 
- `a → a →` 동일 타입의 첫 번째 인자와 두 번째 인자를 받는다.
- `→ Boolean` 첫 번째 인자와 두 번째 인자의 순서가 있으므로 `첫 번째 인자 <= 두 번째 인자` 연산을 수행한 뒤 결과 값을 불리언 타입으로 반환한다.

## 예제
```
R.lte(2, 1); //=> false
R.lte(2, 2); //=> true
R.lte(2, 3); //=> true
R.lte('a', 'z'); //=> true
R.lte('z', 'a'); //=> false
```
- 생략

## Reference
- https://ramdajs.com/docs/#lte
