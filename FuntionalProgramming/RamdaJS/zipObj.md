## zipObj
> Creates a new object out of a list of keys and a list of values.
- 리스트의 키와 리스트의 값들로 새로운 오브젝트를 생성한다.
> Key/value pairing is truncated to the length of the shorter of the two lists.
- 키/벨류 쌍은 두 리스트 보다 더 짧은 길이로 줄여진다.
> Note: zipObj is equivalent to pipe(zip, fromPairs).
- 노트: `zipObj`은 `pipe(zip, fromPairs)`와 같다.

### 설명
- 두 배열을 받아 양쪽 배열의 동일한 인덱스의 원소를 프로퍼티-벨류로 하는 오브젝트를 생성한다.

### 표현
```
[String] → [*] → {String: *}
```
- `[String] →`: 첫 번째 인자로 최종 결과물에서 오브젝트의 키로 변환될 값의 리스트를 받는다.
- `→ [*] →`: 두 번째 인자로 임의의 값을 원소로 하는 배열로 받는다.
- `→ {String: *}`: 첫 번째 인자로 받은 리스트를 오브젝트의 키로, 두 번째 인자로 받은 리스트를 오브젝트의 벨류로 하는 오브젝트를 반환한다.

### 예제
```js
R.zipObj(['a', 'b', 'c'], [1, 2, 3]); //=> {a: 1, b: 2, c: 3}
```
- `['a', 'b', 'c']`, `[1, 2, 3]` 두 배열에서 첫 번째로 받은 베열에서는 키를 뽑아내고, 두 번째로 받은 배열에서는 벨류를 뽑아낸다. 0번 인덱스는 'a'와 1이다. {key: value} 관계는 {'a': 1}이 된다. 1번 인덱스는 'b'와 2이다. {key: value} 관계는 {'b': 2}이 된다. 2번 인덱스는 'c'와 3이다. {key: value} 관계는 {'c': 3}이 된다. 이 키 벨류 관계를 모두 갖는 오브젝트는 `{a: 1, b: 2, c: 3}`이다.

## References
- https://ramdajs.com/docs/#zipObj
