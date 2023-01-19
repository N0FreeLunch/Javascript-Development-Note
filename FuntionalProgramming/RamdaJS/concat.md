## concat
> Returns the result of concatenating the given lists or strings.
- 주어진 리스트들 또는 문자열들을 연쇄 결합한 결과를 반환한다.

> Note: R.concat expects both arguments to be of the same type, unlike the native Array.prototype.concat method.
- 노트: JS의 네이티브 함수인 `Array.prototype.concat` 메소드와 달리 `R.concat` 함수는 두 인자가 동일한 타입일 것을 기대한다.

> It will throw an error if you concat an Array with a non-Array value.
- `R.concat`함수로 배열과 비배열의 값을 연결한다면 에러를 던진다.

> Dispatches to the concat method of the first argument, if present. Can also concatenate two members of a fantasy-land compatible semigroup.
- `concat` 메소드로 첫 번째 인자가 전달되어 실행이 되면, 다음 인자로는 fantasy-land compatible semigroup에 해당하는 대수적 구조를 만족하는 인자를 받아야 한다.

## 설명
- 같은 타입의 문자열 또는 배열을 두 개 받아 원소를 서로 합친 리스트를 반환한다.
- 배열을 받았을 때는 첫 번재 배열의 원소의 나열에 두 번째 배열의 원소 나열을 추가한 원소 리스트를 배열로 반환하며
- 문자열을 받았을 때는 첫 번째 문자열의 문자 나열에 두 번째 문자열의 문자나열을 추가한 문자 리스트를 문자열로 반환한다.
- 두 인자는 리스트의 원소 나열로 기존의 나열된 원소에 추가로 원소를 나열한 리스트를 반환하는 연산을 가지므로 두 인자의 타입이 동일하지 않다면 연산이 성립하지 않으므로 에러를 발생시킨다.
- `concat`은 두 인자의 대수적인 연산을 수행하므로 그 결과값도 동일한 연산으로 사용될 수 있는 인자가 되어야 한다. 따라서 문자열끼리의 연산이라면 문자열을 반환하고, 배열끼리의 연산이라면 배열을 반환하도록 구성되어 있다.

## 표현
```
[a] → [a] → [a]
```
- `[a] → ` 첫 번째 인자로 배열을 받았을 경우
- `→ [a] →` 두 번째 인자로도 배열을 받아야 하며
- `→ [a]` 첫 번째 인자와 두 번째 인자를 연결한 배열이 반환된다.
```
String → String → String
```
- `String →` 첫 번째 인자로 문자열을 받았을 경우
- `→ String →` 두 번째 인자로도 문자열을 받아야 하며
- `→ String` 첫 번째 인자와 두 번째 인자를 연결한 문자열이 반환된다.

## 예제
```
R.concat('ABC', 'DEF'); // 'ABCDEF'
R.concat([4, 5, 6], [1, 2, 3]); //=> [4, 5, 6, 1, 2, 3]
R.concat([], []); //=> []
```
- `R.concat('ABC', 'DEF')` 첫 번째 인자로 문자열을 받았으므로 두 번째 인자도 문자열을 받아야 한다. 두 문자열을 `'ABC'`, `'DEF'`을 결합한 결과인 `[4, 5, 6, 1, 2, 3]`를 반환한다.
- `R.concat([4, 5, 6], [1, 2, 3])` 첫 번째 인자로 배열을 받았으므로 두 번째 인자로 배열을 받아야 한다. 두 배열의 원소를 나열하면 `4, 5, 6, 1, 2, 3` 이고 배열로 반환하므로 `[4, 5, 6, 1, 2, 3]`를 반환한다.
- `R.concat([], [])` 첫 번째 인자로 배열을 받았으므로 두 번째 인자로도 배열을 받아야 한다. 두 배열의 원소를 나열하면 비어있고 이를 배열로 반환하면 `[]` 빈 배열이 반환된다.

## Reference
- https://ramdajs.com/docs/#concat
