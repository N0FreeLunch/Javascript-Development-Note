## trim
> Removes (strips) whitespace from both ends of the string.
- 문자열 얄 끝에서 여백 문자(whitespace)를 제거한다.

### 설명
- 공백 문자 상당에 해당하는 대상을 문자열 양 끝에서 제거한다. 이 때 공백 상당 문자가 연속되는 경우 연속되는 모든 공백문자를 함께 제거한다.

### 표현
```
String → String
```
- `String →`: 첫 번째 인자로 문자열을 받는다.
- `→ String`: 인자로 받은 문자열에서 문자열 양 끝에 연속되는 공백에 해당하는 모든 문자를 제거한다.

### 예제
```js
R.trim('   xyz  '); //=> 'xyz'
R.map(R.trim, R.split(',', 'x, y, z')); //=> ['x', 'y', 'z']
```
- `R.trim('   xyz  ')`: 문자열 `'   xyz  '`의 양 끝에서 연속되는 공백을 제거하면 `'xyz'`가 된다.
- `R.map(R.trim, R.split(',', 'x, y, z'))`: `R.map(함수, 리스트)`의 꼴이다. 리스트로는 `R.split(',', 'x, y, z')`가 주어졌으며, `'x'`, `' y'`, `' z'`으로 y, z 앞에는 공백 문자 하나가 포함되어 있다. 이 배열을 공백 문자 없는 문자열로 변환하고자 할 때, 각각의 원소에 대해 빈 문자열을 반환하는 `R.trim` 함수를 사용해 배열을 순회하여 각 순회에서 반환된 결과 값을 모아 `['x', 'y', 'z']` 값을 얻는다.

## Referecnes
- https://ramdajs.com/docs/#trim
