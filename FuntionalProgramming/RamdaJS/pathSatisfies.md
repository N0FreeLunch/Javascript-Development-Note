## pathSatisfies
> Returns true if the specified object property at given path satisfies the given predicate; false otherwise.
- 주어진 경로의 특정한 오브젝트의 프로퍼티가 주어진 조건을 만족할 때 true를 반환하고, 그렇지 않으면 false를 반환한다.

> See also propSatisfies, path.

### 설명
- 오브젝트 내부의 경로에 해당하는 값이 술어함수를 만족하면 true, 아니면 false를 반환한다.
- 첫 번째 인자로는 취득한 값의 참/거짓을 판단하는 술어함수를 받는다. 이 함수의 결과 값은 최종적으로 반환되는 값이 된다.
- 두 번째 인자로는 대상 오브젝트에서 접근할 프로퍼티를 나열한 배열을 받는다.
- 세 번째 인자로는 대상 오브젝트를 받는다.
- 반환 값으로는 오브젝트에서 주어진 경로에 해당하는 프로퍼티로 접근하여 취득한 값을 첫 번째 인자의 술어함수의 인자로 넣었을 때 반환되는 값을 얻는다.

### 표현
```
(a → Boolean) → [Idx] → {a} → Boolean
Idx = String | Int | Symbol
```
- `(a → Boolean) →`: 첫 번째 인자로 술어 함수를 받는다. 이 술어 함수는 하나의 인자를 받는데 오브젝트의 경로에서 선택된 대상을 뽑아야 하기 때문이다.
- `→ [Idx] →`: 두 번째 인자로 오브젝트의 키에 해당하는 값(`Idx = String | Int | Symbol`)이 나열된 배열을 받는다.
- `→ {a} →`: 세 번째 인자로 오브젝트를 받고, 해당 오브젝트에서 두 번째 인자에서 받은 경로의 원소에 해당하는 프로퍼티에 접근하여 경로의 프로퍼티를 선택해 그 값을 뽑아낸다.
- `Boolean`: 뽑아낸 값을 첫 번째 인자로 받은 술어 함수에 넣어 그 값이 술어함수를 만족하면 true, 만족하지 않으면 false를 반환한다.

### 예제
```js
R.pathSatisfies(y => y > 0, ['x', 'y'], {x: {y: 2}}); //=> true
R.pathSatisfies(R.is(Object), [], {x: {y: 2}}); //=> true
```
- 접근 하려는 경로로 `['x', 'y']`가 주어졌다. `{x: {y: 2}}`에서 주어진 경로에 해당하는 값은 `2`이다. 이 때 이 값을 첫 번째 주어진 술어함수에 통과시켰을 때 `2 > 0`이므로 참이다. 따라서 반환 값은 true이다.
- 접근 하려는 경로로 `[]`으로 빈 배열이 주어졌다. 이는 내부의 대상을 선택만 하며 내부의 값으로는 접근하지 않는다는 의미이다. 따라서 선택된 것은 `{x: {y: 2}}`으로 주어진 오브젝트 그 자체이다. 이를 오브젝트인지 판별하는 술어함수 `R.is(Object)`에 통과 시켰을 때 오브젝트이므로 true를 반환한다.

## Reference
- https://ramdajs.com/docs/#pathSatisfies
