## gte
> Returns true if the first argument is greater than or equal to the second; false otherwise.
- 첫 번째 인자가 두 번째 인자보다 크거나 같으면 참을 반환하고 그렇지 않으면 거짓을 반환한다.

## 표현
```
Ord a => a → a → Boolean
```
- `Ord a =>` 서로 크기 비교가 가능한 종류 a에 대해서
- `a →` 첫 번째 인자로 비교가 가능한 종류의 값을 받는다.
- `→ a →` 두 번째 인자로 비교가 가능한 종류의 값을 받는다.
- `→ Boolean` 첫 번째 인자와 두 번째 인자의 값을 비교하여 첫 번째 인자가 두 번째 인자보다 크거나 같으면 참 아니면 거짓을 반환한다.

## 설명
- 서로 비교가 가능한 두 인자를 받아서 첫 번째 인자가 두 번째 인자보다 크거나 같으면 참 아니면 거짓을 반환한다.

## 예제
```
R.gte(2, 1); //=> true
R.gte(2, 2); //=> true
R.gte(2, 3); //=> false
R.gte('a', 'z'); //=> false
R.gte('z', 'a'); //=> true
```

## Reference
- https://ramdajs.com/docs/#gte
