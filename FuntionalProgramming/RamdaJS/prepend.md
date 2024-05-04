## prepend
> Returns a new list with the given element at the front, followed by the contents of the list.
- 주어진 원소가 가장 앞에 위치한 새로운 리스트를 반환한다. 주어진 원소가 가장 앞에 위치하고 기존 리스트의 원소들이 뒤따른다.

> See also append.

### 설명
- 리스트의 맨 앞에 주어진 원소를 넣은 꼴의 리스트를 반환한다.

### 표현
```
a → [a] → [a]
```
- `a →`: 추가할 대상을 받는다. 이 대상은 두 번째 인자로 받을 `[a]`리스트의 원소로 포함 가능한 대상이어야 한다.
- `→ [a] →`: 두 번째 인자로 리스트를 받는다.
- `→ [a]`: 첫 번째 인자로 받은 대상이 리스트의 첫 번째 원소에 배치된 리스트를 반환한다.

### 예제
```js
R.prepend('fee', ['fi', 'fo', 'fum']); //=> ['fee', 'fi', 'fo', 'fum']
```
- `'fee'` 주어진 인자를 첫 번째 원소로 하고, 기존의 원소들이 그 다음을 뒤따르는 리스트 `['fee', 'fi', 'fo', 'fum']`를 반환한다.

## Reference
- https://ramdajs.com/docs/#prepend
