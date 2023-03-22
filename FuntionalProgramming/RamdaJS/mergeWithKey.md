## mergeWithKey
> Creates a new object with the own properties of the two provided objects. If a key exists in both objects, the provided function is applied to the key and the values associated with the key in each object, with the result being used as the value associated with the key in the returned object.

> See also mergeDeepWithKey, merge, mergeWith.

## 설명

## 표현
```
((String, a, a) → a) → {a} → {a} → {a}
```

## 예시
```
let concatValues = (k, l, r) => k == 'values' ? R.concat(l, r) : r
R.mergeWithKey(concatValues,
               { a: true, thing: 'foo', values: [10, 20] },
               { b: true, thing: 'bar', values: [15, 35] });
//=> { a: true, b: true, thing: 'bar', values: [10, 20, 15, 35] }
```

## Reference
- https://ramdajs.com/docs/#mergeWithKey
