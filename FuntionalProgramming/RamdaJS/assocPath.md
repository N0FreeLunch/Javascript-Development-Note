## assocPath

> Makes a shallow clone of an object
- 오브젝트의 앝은 복사를 한다.

> setting or overriding the nodes required to create the given path and placing the specific value at the tail end of that path.
- 주어진 경로에 해당하는 프로퍼티의 값을 오버라이딩 하거나 새로 만든다. 주어진 경로의 끝 부분의(tail end) 프로퍼티의 값을 달리 할당하는 방식이다.

> Note that this copies and flattens prototype properties onto the new object as well.
- 새로운 오브젝트를 만들면서 이 오브젝트에 기존 오브젝트의 프로토타입을 병합(flattens)하고 복사한다.

> All non-primitive properties are copied by reference.
- 모든 비 프리리티브 프로퍼티는 복사된다.

> See also [dissocPath](./dissocPath.md).

### 설명
- 오브젝트의 지정한 경로의 프로퍼티의 값을 생성하거나 교체한다. 경로는 오브젝트의 프로퍼티에 할당된 오브젝트, 해당 오브젝트의 프로퍼티에 할당된 오브젝트의 프로퍼티에 엑세스 할 수 있는 엑세스 프로퍼티의 순서를 나열한 것이다. 마지막에 엑세스 한 프로퍼티의 값을 변경하며, 경로의 마지막에 이르지 못했다면 엑세스 할 수 있도록 오브젝트를 생성한다.
- 첫 번째 인자로는 변경할 프로퍼티를 지정한다. 이때 배열을 통해서 중첩된(nested) 프로퍼티를 지정할 수 있다. `['a']`라면 받은 오브젝트의 a 프로퍼티를 선택하며, `['a', 'b']`라면 받은 오브젝트의 a프로퍼티에 할당된 오브젝트의 b 프로퍼티를 선택하며, `['a', 'b', 'c']`라면 받은 오브젝트의 a 프로퍼티에 할당된 오브젝트의 b 프로퍼티에 할당된 오브젝트의 c 프로퍼티를 선택한다. 지정한 프로퍼티와 값을 추가하거나 오버라이딩한 새로운 오브젝트를 반환한다.
- 프로토타입의 flatten에 관한 내용은 [assoc](./assoc.md) 부분에 설명했으므로 참고하도록 하자.

### 문법
```
R.assocPath(path, val, obj): Object
```
> `path`: the path to set
- `path`: (값을 생성하거나 변경할) 경로를 설정한다.
> `val`: The new value
- `val`: (값을 생성하거나 변경할) 새로운 값이다.
> `obj`: The object to clone
- `obj`: 클론할 오브젝트이다.
> Returns Object A new object equivalent to the original except along the specified path.
- 지정한 경로를 제외하고는 원본과 동등한 새 오브젝트를 반환한다.

### 표현
```
[Idx] → a → {a} → {a}
Idx = String | Int | Symbol
```
- `Idx = String | Int | Symbol`: Idx는 오브젝트의 키로 설정할 수 있는 값이며, 문자열, 정수, 심볼 타입이 위치할 수 있다.
- `[Idx] →`: 첫 번째 인자로 인덱스 값을 받는다. 오브젝트의 프로퍼티명을 배열로 나열하며, 나열한 순서대로 오브젝트의 프로퍼티를 순차적으로 접근한다. 이를 '경로'(path)라하고 한다. 순차적으로 프로퍼티에 엑세스 할 때, 오브젝트가 아니라서 프로퍼티가 없는 경우, 엑세스 할 수 있도록 해당 프로퍼티를 갖는 오브젝트를 생성하여 주어진 경로의 끝까지 도달 할 수 있도록 한다. 배열의 가장 마지막에 나열된 프로퍼티에 세 번째 인자로 받은 값을 할당한다.
- ` → a →`: 두 번째 인자로는 첫 번째 인자의 경로 끝에 할당할 값을 받는다.
- `→ {a} →`: 세 번째 인자로는 대상 오브젝트를 지정한다.
- `→ {a}`: 세 번째 인자로 받은 오브젝트에서 첫 번째 인자의 경로 끝에, 두 번째 인자의 값을 할당하여 새로운 값을 생성하거나 변경한 오브젝트를 반환한다.

### 예제
```js
R.assocPath(['a', 'b', 'c'], 42, {a: {b: {c: 0}}}); //=> {a: {b: {c: 42}}}

// Any missing or non-object keys in path will be overridden
R.assocPath(['a', 'b', 'c'], 42, {a: 5}); //=> {a: {b: {c: 42}}}
```
- 주어진 오브젝트 `{a: {b: {c: 0}}}`에 대해 `['a', 'b', 'c']`로 대상 프로퍼티를 지정한다. a 프로퍼티에 할당된 오브젝트의 b 프로퍼티 할당된 오브젝트의 c 프로퍼티의 값을 `42` 값으로 치환한 결과를 복사하여 반환한다. 따라서 결과는 `{a: {b: {c: 0}}}`가 `{a: {b: {c: 42}}}`가 된 결과가 반환된다.
- 주어진 오브젝트 `{a: 5}`에 대해 `['a', 'b', 'c']`로 대상 프로퍼티를 지정한다. a 프로퍼티에 5가 할당되어 있지만 오브젝트를 오버라이딩하고 b 프로퍼티에도 오브젝트를 추가하고 c 프로퍼티에 값을 할당한다. 따라서 `{a: 5}`가 `{a: {b: {c: 42}}}`으로 된다.

## References
- https://ramdajs.com/docs/#assocPath
- https://github.com/ramda/ramda/blob/master/test/assocPath.js
- https://github.com/ramda/types/blob/develop/types/assocPath.d.ts
