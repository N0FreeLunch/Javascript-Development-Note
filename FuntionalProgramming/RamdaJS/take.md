## take
> Returns the first n elements of the given list, string, or transducer/transformer (or object with a take method).
- 주어진 대상에서 처음 n개의 원소를 반환한다. 대상으로는 리스트, 문자열, transducer/transformer, take 메소드를 갖는 object가 가능하다.

> Dispatches to the take method of the second argument, if present.
- 두 번째 인자에 take 메소드가 있다면, take 메소드를 발동한다.

> See also drop.

### 설명
- 원소의 순서가 정해진 집합에서 가장 앞선 원소 부터 뒤따르는 순서의 원소를 n개만을 갖는 동일한 종류의 집합을 반환한다.
- 예를 들어 배열이라면 배열을 반환하고, 문자열이면 문자열을 반환하는 식이다.

### 표현

#### 배열
```
Number → [a] → [a]
```
- `Number →`: 첫 번째 인자로 취득할 원소의 갯수를 정한다.
- `→ [a] →`: 두 번째 인자로 대상 배열을 받는다.
- `→ [a]`: 대상 배열에서 첫 번째 원소부터 뒤따르는 첫 번째 인자로 받은 수의 갯수 만큼의 원소를 갖는 배열을 받는다.

#### 문자열
```
Number → String → String
```
- `Number →`: 첫 번째 인자로 취득할 원소의 갯수를 정한다.
- `→ String →`: 두 번째 인자로 대상 문자열을 받는다.
- `→ String`: 대상 문자열에서 첫 번째 문자부터 뒤따르는 첫 번째 인자로 받은 수의 갯수 만큼의 원소를 갖는 배열을 받는다.

### 예제

#### 배열에 대한 처리
```js
R.take(1, ['foo', 'bar', 'baz']); //=> ['foo']
R.take(2, ['foo', 'bar', 'baz']); //=> ['foo', 'bar']
R.take(3, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.take(4, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
```
- `R.take(1, ['foo', 'bar', 'baz'])`: `['foo', 'bar', 'baz']`에서 첫 번째 원소부터 뒤따르는 1개의 원소를 가진 배열을 반환한다. 따라서 그 결과는 `['foo']`이다.
- `R.take(2, ['foo', 'bar', 'baz'])`: `['foo', 'bar', 'baz']`에서 첫 번째 원소부터 뒤따르는 2개의 원소를 가진 배열을 반환한다. 따라서 그 결과는 `['foo', 'bar']`이다.
- `R.take(3, ['foo', 'bar', 'baz'])`: `['foo', 'bar', 'baz']`에서 첫 번째 원소부터 뒤따르는 3개의 원소를 가진 배열을 반환한다. 따라서 그 결과는 `['foo', 'bar', 'baz']`이다.
- `R.take(4, ['foo', 'bar', 'baz'])`: `['foo', 'bar', 'baz']`에서 첫 번째 원소부터 뒤따르는 4개의 원소를 가진 배열을 반환한다. 그런데 4번째 원소는 존재하지 않으므로 결과 배열의 원소로 포함하지 않는다. 따라서 그 결과는 `['foo', 'bar', 'baz']`이다.

#### 문자열에 대한 처리
```js
R.take(3, 'ramda');               //=> 'ram'
```
- `R.take(3, 'ramda')`: 문자열에서 첫 번째 문자부터 뒤따르는 4개의 문자를 가진 문자열을 반환한다. 따라서 그 결과는 `'ram'`이다.

#### 원소를 취득할 대상을 따로 받기
```js
const personnel = [
  'Dave Brubeck',
  'Paul Desmond',
  'Eugene Wright',
  'Joe Morello',
  'Gerry Mulligan',
  'Bob Bates',
  'Joe Dodge',
  'Ron Crotty'
];

const takeFive = R.take(5);
takeFive(personnel);
//=> ['Dave Brubeck', 'Paul Desmond', 'Eugene Wright', 'Joe Morello', 'Gerry Mulligan']
```
- `takeFive`에서 두 번째 인자를 전달하지 않는 것으로 첫 번째 부터 뒤따르는 5개의 원소를 가진 대상을 가진 집합을 반환하는 대상을 반환한다.
- `takeFive(personnel)` 배열을 전달하여 배열의 첫 번째 부터 뒤따르는 5개의 원소를 가진 배열을 반환하게 된다. 따라서 8개의 원소 중에서 5개만 갖는 `['Dave Brubeck', 'Paul Desmond', 'Eugene Wright', 'Joe Morello', 'Gerry Mulligan']`가 반환된다.

## Reference
- https://ramdajs.com/docs/#take
