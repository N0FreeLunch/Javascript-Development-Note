## takeLast
> Returns a new list containing the last n elements of the given list. If n > list.length, returns a list of list.length elements.
- 주어진 리스트에서 마지막의 n개의 원소들을 포함한 새로운 리스트를 반환한다. 만약 n이 list.length 값을 초과한다면, list.length 개의 원소의 리스트를 반환한다.

> See also dropLast.

### 설명

### 표현

#### 배열의 경우
```
Number → [a] → [a]
```

#### 문자열의 경우
```
Number → String → String
```

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
