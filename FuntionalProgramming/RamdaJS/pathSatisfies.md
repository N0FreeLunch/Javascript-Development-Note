## pathSatisfies
> Returns true if the specified object property at given path satisfies the given predicate; false otherwise.

> See also propSatisfies, path.

### 설명

### 표현
```
(a → Boolean) → [Idx] → {a} → Boolean
Idx = String | Int | Symbol
```

### 예제
```js
R.pathSatisfies(y => y > 0, ['x', 'y'], {x: {y: 2}}); //=> true
R.pathSatisfies(R.is(Object), [], {x: {y: 2}}); //=> true
```

## Reference
- https://ramdajs.com/docs/#pathSatisfies
