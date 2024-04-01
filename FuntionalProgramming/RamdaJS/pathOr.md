## pathOr
> If the given, non-null object has a value at the given path, returns the value at that path. Otherwise returns the provided default value.
- 어떤 값이 들어 있는 널이 아닌 오브젝트가 주어진 경로에 해당하는 값인 경우 해당 경로의 값을 반환하고 그렇지 않으면 주어진 기본 값을 반환한다.

### 설명
- 오브젝트 내부의 지정한 경로에 해당하는 값을 반환하되, 매칭되지 않으면 `path`가 `undefined`를 반환하는 것과 달리, 함수를 사용할 때 주어진 디폴트 값을 반환한다.
- 첫 번째 인자로 반환할 디폴트 값을 지정하며, 두 번째 인자로 경로를 의미하는 배열을 받고, 세 번째 인자로 탐색할 대상 오브젝트를 받는다.

### 표현
```
a → [Idx] → {a} → a
Idx = String | Int | Symbol
```
- `Idx = String | Int | Symbol`: 오브젝트의 키로 사용할 수 있는 타입으로 오브젝트의 내부의 경로를 지정하는데 사용한다.

## 예제
```js
R.pathOr('N/A', ['a', 'b'], {a: {b: 2}}); //=> 2
R.pathOr('N/A', ['a', 'b'], {c: {b: 2}}); //=> "N/A"
```

## Reference
- https://ramdajs.com/docs/#pathOr
