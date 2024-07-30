## takeLast
> Returns a new list containing the last n elements of the given list. If n > list.length, returns a list of list.length elements.
- 주어진 리스트에서 마지막의 n개의 원소들을 포함한 새로운 리스트를 반환한다. 만약 n이 list.length 값을 초과한다면, list.length 개의 원소의 리스트를 반환한다.

> See also dropLast.

### 설명
- `R.take` 함수가 첫 번째 원소부터 n개의 원소를 갖는 집합(배열, 문자열)을 반환하는 것과 달리 `R.takeLast` 함수는 마지막 원소 부터 n개째의 원소부터 마지막 원소까지 원소를 나열한 집합을 반환한다. 즉, 마지막 부터 n개의 원소를 갖는 집합을 반환하되 그 순서를 유지한다는 의미를 갖는다.

### 표현

#### 배열의 경우
```
Number → [a] → [a]
```
- `Number →`: 첫 번째 인자로 뽑을 원소의 갯수를 받는다.
- `→ [a] →`: 두 번째 인자로 대상 배열을 받는다.
- `→ [a]`: 두 번째 인자의 배열에서 첫 번째 인자로 받은 수 만큼의 원소를 동일한 순서로 나열한 배열을 반환한다.

#### 문자열의 경우
```
Number → String → String
```
- `Number →`: 첫 번째 인자로 뽑을 문자의 수를 지정한다.
- `→ String →`: 두 번째 인자로 대상 문자열을 받는다.
- `→ String`: 두 번째로 인자의 문자열에서 첫 번째 인자로 받은 수 만큼의 문자를 동일한 순서로 나열한 문자열을 반환한다.

### 예제
```js
R.takeLast(1, ['foo', 'bar', 'baz']); //=> ['baz']
R.takeLast(2, ['foo', 'bar', 'baz']); //=> ['bar', 'baz']
R.takeLast(3, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.takeLast(4, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.takeLast(3, 'ramda');               //=> 'mda'
```
- `R.takeLast(1, ['foo', 'bar', 'baz'])`: `['foo', 'bar', 'baz']`에서 마지막 원소부터 1개의 원소를 순서 그대로 뽑아 `'baz'`를 갖는 배열을 반환한다.
- `R.takeLast(2, ['foo', 'bar', 'baz'])`: `['foo', 'bar', 'baz']`에서 마지막 원소부터 2개의 원소를 순서 그대로 뽑아 `'bar', 'baz'`를 갖는 배열을 반환한다.
- `R.takeLast(3, ['foo', 'bar', 'baz'])`: `['foo', 'bar', 'baz']`에서 마지막 원소부터 3개의 원소를 순서 그대로 뽑아 `'foo', 'bar', 'baz'`를 갖는 배열을 반환한다.
- `R.takeLast(4, ['foo', 'bar', 'baz'])`: `['foo', 'bar', 'baz']`에서 마지막 원소부터 4개의 원소를 순서 그대로 뽑는데 원소 수를 초과하므로 최대 원소 개수만 뽑아 `'foo', 'bar', 'baz'`를 갖는 배열을 반환한다.
- `R.takeLast(3, 'ramda')`: `'ramda'`에서 마지막 문자부터 3개의 문자를 순서 그대로 뽑아 `'mda'`의 문자열을 반환한다.

## Reference
- https://ramdajs.com/docs/#takeLast
