## assocPath
- R.assocPath
> Makes a shallow clone of an object
- 오브젝트를 앝은 복사를 한다.
> setting or overriding the nodes required to create the given path and placing the specific value at the tail end of that path.
- 주어진 경로에 해당하는 프로퍼티의 값을 오버라이딩 하거나 새로 만든다. 주어진 경로의 끝 부분의 프로퍼티의 값을 달리 할당하는 방식이다.
> Note that this copies and flattens prototype properties onto the new object as well.
- 새로운 오브젝트를 만들면서 이 오브젝트에 기존 오브젝트의 프로토타입을 병합(flattens)하고 복사한다.
>  All non-primitive properties are copied by reference.
- 모든 비 프리리티브 프로퍼티는 복사된다. 


## 표현
```
[Idx] → a → {a} → {a}
Idx = String | Int | Symbol
```
- `[Idx]` 프로퍼티명을 배열로 지정하며, 배열의 첫 번째 원소 부터 차례로 주어진 오브젝트의 프로퍼티를 중첩하는 방식으로 선택한다.
- ` → a →` 두 번째 인자로는 프로퍼티에 지정할 값을 받는다.
- `→ {a} →` 

## 설명
- 첫 번째 인자로는 변경할 프로퍼티를 지정한다. 이때 배열을 통해서 중첩된(nested) 프로퍼티를 지정할 수 있다.
- `['a']`라면 받은 오브젝트의 a 프로퍼티를 선택하며, `['a', 'b']`라면 받은 오브젝트의 a프로퍼티에 할당된 오브젝트의 b 프로퍼티를 선택하며, `['a', 'b', 'c']`라면 받은 오브젝트의 a 프로퍼티에 할당된 오브젝트의 b 프로퍼티에 할당된 오브젝트의 c 프로퍼티를 선택한다.
- 두 번째 인자로는 지정한 프로퍼티에 넣을 값을 선택한다.
- 세번째 인자로는 대상 오브젝트를 지정한다.
- 지정한 프로퍼티와 값을 추가하거나 오버라이딩한 새로운 오브젝트를 반환한다.


## 예제
```
R.assocPath(['a', 'b', 'c'], 42, {a: {b: {c: 0}}}); //=> {a: {b: {c: 42}}}

// Any missing or non-object keys in path will be overridden
R.assocPath(['a', 'b', 'c'], 42, {a: 5}); //=> {a: {b: {c: 42}}}
```
- 주어진 오브젝트 `{a: {b: {c: 0}}}`에 대해 `['a', 'b', 'c']`로 대상 프로퍼티를 지정한다. a 프로퍼티에 할당된 오브젝트의 b 프로퍼티 할당된 오브젝트의 c 프로퍼티의 값을 `42` 값으로 치환한 결과를 복사하여 반환한다. 따라서 결과는 `{a: {b: {c: 0}}}`가 `{a: {b: {c: 42}}}`가 된 결과가 반환 됨
- 주어진 오브젝트 `{a: 5}`에 대해 `['a', 'b', 'c']`로 대상 프로퍼티를 지정한다. a 프로퍼티에 5가 할당되어 있지만 오브젝트를 오버라이딩하고 b 프로퍼티에도 오브젝트를 추가하고 c 프로퍼티에 값을 할당한다. 따라서 `{a: 5}`가 `{a: {b: {c: 42}}}`으로 됨


## Reference
- https://ramdajs.com/docs/#assocPath
