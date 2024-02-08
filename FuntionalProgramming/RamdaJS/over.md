## over
> Returns the result of "setting" the portion of the given data structure focused by the given lens to the result of applying the given function to the focused value.

> See also view, set, lens, lensIndex, lensProp, lensPath.

### 설명
```
Lens s a → (a → a) → s → s
Lens s a = Functor f => (a → f a) → s → f s
```

### 표현

### 예제
```js
const headLens = R.lensIndex(0);

R.over(headLens, R.toUpper, ['foo', 'bar', 'baz']); //=> ['FOO', 'bar', 'baz']
```

## Reference
- https://ramdajs.com/docs/#over
