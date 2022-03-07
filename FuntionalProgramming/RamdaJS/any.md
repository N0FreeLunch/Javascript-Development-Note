## any
- R.any()

## 설명
- `R.any(술어함수)(리스트);`
- 리스트로의 원소들이 하나라도 주어진 술어함수를 만족하는지 확인하는 함수


## 표현
```
(a → Boolean) → [a] → Boolean
```


## 예제
```
const lessThan0 = R.flip(R.lt)(0);
const lessThan2 = R.flip(R.lt)(2);
R.any(lessThan0)([1, 2]); //=> false
R.any(lessThan2)([1, 2]); //=> true
```
- `R.lt`은 첫 번째 인자 보다 두 번째 인자가 클 때 true를 반환
- `R.flip` 리스트의 첫번째 원소와 두 번째 원소의 순서를 바꾼다.

## Reference
- https://ramdajs.com/docs/#any
