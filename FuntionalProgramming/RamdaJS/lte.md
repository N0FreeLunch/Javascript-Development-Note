## lte
> Returns true if the first argument is less than or equal to the second; false otherwise.
- 첫 번째인자가 두 번째 인자보다 작거나 같다면 참을 아니면 거짓을 반환한다.

## 표현
```
Ord a => a → a → Boolean
```
- `Ord a =>` 순서를 가진 타입 a에 대하여
- `a → a →` 첫 번째 인자와 두 번째 인자를 받아 두 인자의 순서를 비교하여
- `→ Boolean` `첫 번째 인자 <= 두 번째 인자`이면 참 아니면 거짓을 반환한다.

## 설명
- 달리 설명이 필요없다.

## 예제
```
R.lte(2, 1); //=> false
R.lte(2, 2); //=> true
R.lte(2, 3); //=> true
R.lte('a', 'z'); //=> true
R.lte('z', 'a'); //=> false
```
- 예제만으로 충분하므로 넘어간다.

## Reference
- https://ramdajs.com/docs/#lte
