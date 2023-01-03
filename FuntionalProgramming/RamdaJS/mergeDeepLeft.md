## mergeDeepLeft
> Creates a new object with the own properties of the first object merged with the own properties of the second object. If a key exists in both objects:
- 두번째 오브젝트가 가진 프로퍼티들에 첫 번째 오브젝트가 가진 프로퍼티가 합쳐진(merged) 새로운 오브젝트를 반환한다. 만약 동일한 키가 양쪽에 있다면 
> and both values are objects, the two values will be recursively merged
- 양쪽의 값이 오브제트라면 두 값을 재귀적으로 합친 값을
> otherwise the value from the first object will be used.
- 양쪽의 값이 오브젝트가 아니라면 첫 번째 오브젝트의 프로퍼티를 사용한다.
> See also merge, mergeDeepRight, mergeDeepWith, mergeDeepWithKey.

## 설명
- 두 오브젝트를 받아 프로퍼티를 합친다. 이때 인자가 나열된 순에서 왼쪽의 프로퍼티를 우선하여 합친다. 만약 두 오브젝트의 동일한 프로퍼티의 값이 오브젝트라면 재귀적으로 합쳐진 오브젝트를 프로퍼티의 값으로 갖는다.

## 표현
```
{a} → {a} → {a}
```
- `{a} →` 첫 번째 인자로 오브젝트를 받고
- `→ {a} →` 두 번째 인자로 오브젝트를 받는다.
- `→ {a}` 반환된 값은 두 오브젝트의 프로퍼티를 합친 결과를 받고 프로퍼티의 우선순위는 왼쪽의 인자 곧 첫 번째 오브젝트를 우선시하여 합쳐진다.

## 예제
```
R.mergeDeepLeft({ name: 'fred', age: 10, contact: { email: 'moo@example.com' }},
                { age: 40, contact: { email: 'baa@example.com' }});
//=> { name: 'fred', age: 10, contact: { email: 'moo@example.com' }}
```
- `name`은 두 오브젝트 모두에 존재하므로 첫 번째 인자의 것을, `age`도 두 오브젝트 모두에 존재하므로 첫 번째 인자의 것을 사용하며 `contact`는 두 오브젝트 모두에 존재하지만 양쪽이 오브젝트이므로 재귀적으로 두 오브젝트가 합성되어야 하지만 두 오브젝트가 동일한 프로퍼티를 가지고 있으므로 첫 번째 오브젝트의 `contact`값에 존재하는 프로퍼티가 우선시 된다.

## Reference
- https://ramdajs.com/docs/#mergeDeepLeft
