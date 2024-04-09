## paths
> Retrieves the values at given paths of an object.
- 오브젝트에서 주어진 경로의 값을 취득한다.

> See also path.

### 설명
- path와 달리 첫 번째 인자로 배열을 원소로 하는 배열을 받는다. 배열 안에 나열된 배열 각각은 경로를 나타내며, 경로를 나타내는 각각의 배열에 대응하는 결과값을 얻으므로 반환 값은 배열이며 반환 배열의 원소는 각각의 경로 배열에 의해 오브젝트에서 취득한 결과값이 된다.
- 첫 번째 인자로 배열을 받는다. 이 배열에는 여러 배열이 들어 있으며 각각의 배열은 오브젝트에서 순차적으로 접근할 키를 나열하고 있다.
- 두 번째 인자로 대상 오브젝트를 받는다.

### 문법
```
[Idx] → {a} → [a | Undefined]
Idx = [String | Int | Symbol]
```

### 예제
```js
R.paths([['a', 'b'], ['p', 0, 'q']], {a: {b: 2}, p: [{q: 3}]}); //=> [2, 3]
R.paths([['a', 'b'], ['p', 'r']], {a: {b: 2}, p: [{q: 3}]}); //=> [2, undefined]
```

### Reference
- https://ramdajs.com/docs/#paths
