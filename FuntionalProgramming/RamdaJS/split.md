## split
> Splits a string into an array of strings based on the given separator.
- 어떤 문자열을 나누어 배열로 만든다. 이때 배열의 (원소가 되는) 문자열은 주어진 구분자(separator)에 의해 나눠진다.

> See also join.

### 설명
- 문자열 또는 정규 표현식을 기준으로 문자열을 나눠서 생긴 문자열을 배열로 반환한다.
- 이 때 분리된 문자열은 문자열의 앞 부분의 문자열이 반환되는 배열의 앞쪽 인덱스에 배치가 되어 반환된다.

### 표현
```
(String | RegExp) → String → [String]
```
- `(String | RegExp) →`: 첫 번째 인자로 문자열 또는 정규 표현식을 받는다.
- `→ String →`: 두 번째 인자로 대상 문자열을 받는다.
- `→ [String]`: 나눠진 문자열을 배열로 모아 반환한다.

### 예제
```js
const pathComponents = R.split('/');
R.tail(pathComponents('/usr/local/bin/node')); //=> ['usr', 'local', 'bin', 'node']

R.split('.', 'a.b.c.xyz.d'); //=> ['a', 'b', 'c', 'xyz', 'd']
```
#### 경로 분류의 예
- `'/'`을 기준으로 문자열을 나누도록 구분자(separator)를 설정한다.
- `pathComponents('/usr/local/bin/node')`는 `'/'`을 기준으로 문자열을 나누어 `['', 'usr', 'local', 'bin', 'node']`가 된다.
- `R.tail` 함수는 배열을 받아서 첫 번째 인자를 제외한 나머지를 새로운 배열로 반환하는 함수이다. 따라서 `R.tail(pathComponents('/usr/local/bin/node'))`는 `R.tail(['', 'usr', 'local', 'bin', 'node'])`이므로 결과는 `['usr', 'local', 'bin', 'node']`가 된다.

#### 닷으로 연결된 문자열을 분리
- `R.split('.', 'a.b.c.xyz.d')` 닷(`.`)을 기준으로 `'a.b.c.xyz.d'`를 분리하면 `['a', 'b', 'c', 'xyz', 'd']`가 된다.

## Reference
- https://ramdajs.com/docs/#split
