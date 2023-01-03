## mergeDeepRight
> Creates a new object with the own properties of the first object merged with the own properties of the second object. If a key exists in both objects:

> and both values are objects, the two values will be recursively merged
> otherwise the value from the second object will be used.
> See also merge, mergeDeepLeft, mergeDeepWith, mergeDeepWithKey.

## 설명
- 두 오브젝트를 받아 프로퍼티를 합친다. 이때 인자가 나열된 순에서 오른쪽의 프로퍼티를 우선하여 합친다. 만약 두 오브젝트의 동일한 프로퍼티의 값이 오브젝트라면 재귀적으로 합쳐진 오브젝트를 프로퍼티의 값으로 갖는다.
- `mergeDeepLeft`와 인자의 우선순위가 반대이다. 이므로 상세한 설명은 생략한다.

## 표현
```
{a} → {a} → {a}
```

## 예제
```
R.mergeDeepRight({ name: 'fred', age: 10, contact: { email: 'moo@example.com' }},
                 { age: 40, contact: { email: 'baa@example.com' }});
//=> { name: 'fred', age: 40, contact: { email: 'baa@example.com' }}
```

## Reference
- https://ramdajs.com/docs/#mergeDeepRight
