## update
> Returns a new copy of the array with the element at the provided index replaced with the given value.
- 배열의 지정한 인덱스를 주어진 값으로 대체한 복사본을 반환한다.

> See also adjust.

### 설명
- 인덱스 번호와 값을 받아서 대상 배열의 인덱스 값을 주어진 값으로 대체한 복사된 배열을 반환한다.

### 표현
```
Number → a → [a] → [a]
```
- `Number →`: 첫 번째 인자로 인덱스 번호를 받는다.
- `→ a →`: 두 번째 인자로 대상 값을 받는다. 대체할 데이터의 일관성을 위해서 동일한 종류의 값 `a`를 대상으로 한다.
- `→ [a] →`: 세 번째 인자로 대상 배열을 받는다.
- `→ [a]`: 대상 배열의 지정한 인덱스 번호의 값을 지정한 값으로 바꾼 배열을 반환한다.

### 예제
```js
R.update(1, '_', ['a', 'b', 'c']);      //=> ['a', '_', 'c']
R.update(-1, '_', ['a', 'b', 'c']);     //=> ['a', 'b', '_']
```
- `R.update(1, '_', ['a', 'b', 'c'])`: 1번 인덱스 `'b'` 값을 `'_'`으로 치환한 배열을 반환한다. 따라서 `['a', '_', 'c']`이다.
- `R.update(-1, '_', ['a', 'b', 'c'])`: -1번 인덱스 `'c'` 값을 `'_'`으로 치환한 배열을 반환한다. 따라서 `['a', 'b', '_']`이다.

### References
- https://ramdajs.com/docs/#update
