## gt

> Returns true if the first argument is greater than the second; false otherwise.
- 만약 첫번째 인자가 두번째 인자보다 크다면 true를 반환하고 그렇지 않으면 false를 반환한다.

## 설명

첫 번째 인자를 A, 두 번째 인자를 B라고 하면, A > B이면 참 아니면 거짓이 된다.

## 표현

```
Ord a => a → a → Boolean
```

- `Ord a`: a 타입은 이 타입에 속하는 값이 순서를 가지고 있다는 것.
- `a →`: 첫 번째 인자로 순서를 가진 값을 넣고
- `→ a →`: 두 번째 인자로 순서를 가진 값을 넣는다.
- 첫 번째 인자와 두 번째 인자의 순서를 비교한 결과를 불리언 형식의 값으로 반환한다.

## 예제

```js
R.gt(2, 1); //=> true
R.gt(2, 2); //=> false
R.gt(2, 3); //=> false
R.gt('a', 'z'); //=> false
R.gt('z', 'a'); //=> true
```
- `R.gt(2, 1)` 2가 1보다 크기 때문에 true
- `R.gt(2, 2)` 2가 2보다 클 수 없기 때문에 false
- `R.gt(2, 3)` 2가 3보다 크지 않기 때문에 false
- `R.gt('a', 'z')` 문자열 번호 a가 문자열 번호 z보다 크지 않기 때문에 false
- `R.gt('z', 'a')` 문자열 번호 z가 문자열 번호 a보다 크기 때문에 true

## References

- https://ramdajs.com/docs/#gt
- https://github.com/ramda/ramda/blob/master/test/gt.js
- https://github.com/ramda/types/blob/develop/types/gt.d.ts
