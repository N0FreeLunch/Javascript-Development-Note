## lt
> Returns true if the first argument is less than the second; false otherwise.
- 만약 첫 번째 인자가 두 번째 인자보다 작으면 true를 반환하고 그렇지 않으면 false를 반환한다.

## 표현
```
Ord a => a → a → Boolean
```
- `Ord a` 타입 a의 원소는 순서를 가진다.
- `a →` 첫 번째 인자로 순서를 가진 값을 받는다.
- `→ a →` 두 번째 인자로 순서를 가진 값을 받는다.
- 두 인자의 순서를 비교하여 그 결과를 불리언 형식으로 반환한다.


## 예제
```
R.lt(2, 1); //=> false
R.lt(2, 2); //=> false
R.lt(2, 3); //=> true
R.lt('a', 'z'); //=> true
R.lt('z', 'a'); //=> false
```
- `R.lt(2, 1)` 2보다 1이 작지 않으므로 false
- `R.lt(2, 2)` 2보다 2가 작지 않으므로 false
- `R.lt(2, 3)` 2보다 3이 작으므로 true
- `R.lt('a', 'z')` 
- `R.lt('z', 'a')`

## Reference
- https://ramdajs.com/docs/#lt
