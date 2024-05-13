## range
> Returns a list of numbers from from (inclusive) to to (exclusive).
- 시작점(시작점은 포함한다: 이상)에서 끝점(끝점은 포함하지 않는다: 미만)까지의 수들의 리스트를 반환한다.

### 설명
- 시작점 이상 끝점 미만에 해당하는 정수 리스트를 반환한다.

### 표현
```
Number → Number → [Number]
```
- `Number →`: 첫 번째 인자로 시작점을 지정한다.
- `→ Number →`: 두 번째 인자로 끝점을 지정한다.
- `→ [Number]`: 시작점 이상 끝점 미만의 정수 리스트를 반환한다.

### 예제
```js
R.range(1, 5);    //=> [1, 2, 3, 4]
R.range(50, 53);  //=> [50, 51, 52]
```
- 1이상 5미만의 수를 나열한 리스트를 반환한다.
- 50이상 53미만의 수를 나열한 리스트를 반환한다.

## Reference
- https://ramdajs.com/docs/#range
