## mean
> Returns the mean of the given list of numbers.
- 원소가 수로 이뤄진 리스트의 평균값을 반환한다.

> See also median.

## 설명
- 주어진 리스트 내의 모든 수들의 평균값을 반환한다.

## 표현
```
[Number] → Number
```
- `[Number] →` 첫 번째 인자로 원소가 Number 타입의 수로 구성된 배열을 받는다. 
- `→ Number` 첫 번째 인자로 받은 리스트의 원소들의 평균값을 반환한다.

## 예제
```
R.mean([2, 7, 9]); //=> 6
R.mean([]); //=> NaN
```
- `R.mean([2, 7, 9])` `(2+7+9)/3 = 6`이다.
- `R.mean([])` 평균값을 구할 수 없다면 `NaN`을 반환한다.

## Reference
- https://ramdajs.com/docs/#mean
