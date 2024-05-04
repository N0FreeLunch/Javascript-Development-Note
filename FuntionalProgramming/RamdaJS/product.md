## product
> Multiplies together all the elements of a list.
- 리스트의 모든 원소들을 곱한 결과를 반환한다.

> See also reduce.

### 설명
- 주어진 리스트의 모든 원소들의 곱셈 결과를 반환한다.
- 총 가격을 계산할 때 유용하다.

### 표현
```
[Number] → Number
```
- `[Number] → ` 첫 번째 인자로 수의 리스트를 받는다.
- `→ Number`: 모든 원소(수)를 곱한 결과를 반환한다.

### 예제
```
R.product([2,4,6,8,100,1]); //=> 38400
```
- 2 x (2 x 2) x (2 x 3) x (2 x 2 x 2) x 100 x 1 = 2^7 x 3 x 100 x 1 = 128 x 3 x 100 = (130 - 2) x 3 x 100 = (390 - 6) x 100 = 38400
 
## Reference
- https://ramdajs.com/docs/#product
