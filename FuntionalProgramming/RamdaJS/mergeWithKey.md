## mergeWithKey
> Creates a new object with the own properties of the two provided objects.
- 제공된 두 오브젝트의 고유한 속성을 가진 하나의 새로운 오브젝트를 생성합니다.
> If a key exists in both objects, the provided function is applied to the key and the values associated with the key in each object,
- 두 객체에 공통으로 존재하는 키가 있다면, 제공된 함수는 각각의 오브젝트의 키와 해당 키에 연관된 값에 적용됩니다. 
> with the result being used as the value associated with the key in the returned object.
- 한수의 연산 결과는 반환된 오브젝트의 키에 연관된 벨류에 사용됩니다.

> See also mergeDeepWithKey, merge, mergeWith.

## 설명
- 두 오브젝트 각각이 가진 키와 키에 대응하는 벨류를 모두 포함하는 새로운 오브젝트를 만든다. 이 때, 두 오브젝트의 키가 중복될 경우 중복된 키의 벨류를 어떻게 머지 함수의 결과 오브젝트에 포함할 것인지를 결정하는 결정함수를 받는다.
- 첫 번째 인자로는 결정함수를 받으며 이 결정함수는 첫 번째 파라메터로 키, 두 번째 파라메터로 첫 번째 오브젝트의 첫 번재 파라메터에 할당된 키에 연관되는 벨류, 세 번째 파라메터로 두 번째 오브젝트의 첫 번재 파라메터에 할당된 키에 연관되는 벨류를 받는다.

## 표현
```
((String, a, a) → a) → {a} → {a} → {a}
```
- `(String, a, a) → a)` 첫 번째 인자로 결정함수를 받는다. 이 결정함수는 첫 번째 파라메터로 키를 지정할 수 있는 문자열을 받고, 두 번째와 세 번째 인자로 파라메터로 키에 해당하는 벨류값을 받으므로 어느 타입이라도 받을 수 있다.
- `→ {a} →` 두 번째 인자로 어떤 오브젝트를 받는다.
- `→ {a} →` 세 번째 인자로 두 번째 인자로 받은 오브젝트와 통합할 오브젝트를 받는다.
- `→ {a}` 두 번째 인자로 받은 오브젝트와 세 번째 인자로 받은 오브젝트를 통합하는 오브젝트를 받는다.

## 예시
```
let concatValues = (k, l, r) => k == 'values' ? R.concat(l, r) : r
R.mergeWithKey(concatValues,
               { a: true, thing: 'foo', values: [10, 20] },
               { b: true, thing: 'bar', values: [15, 35] });
//=> { a: true, b: true, thing: 'bar', values: [10, 20, 15, 35] }
```
- `(k, l, r) => k == 'values' ? R.concat(l, r) : r`에서 `k`는 두 객체 모두에 존재하는 키에 해당하며, `l`은 첫 번째 오브젝트의 키에 연관된 값이며, `r`은 두 번째 오브젝트의 키에 연관된 값이다. 만얄 두 오브젝트에 존재하는 키 값이 `'values'` 문자열과 같다면 두 오브젝트의 전달받는 키인 `k`에 연관되는 값인 `l`과 `r`은 `R.concat(l, r)`에 따라 합쳐지고, 두 오브젝트 모두에 존재하는 키 값이 `'values'`와 같지 않다면 두 번째 오브젝트의 키 `k`에 연관 된 값인 `r`이 반환된다는 의미이다.
- 두 오브젝트 `{ a: true, thing: 'foo', values: [10, 20] }`와 `{ b: true, thing: 'bar', values: [15, 35] }`에서 공통으로 존재하는 키 값은 `thing`와 `values`이고 이 두 키에 대해 `concatValues` 함수가 적용된다. ``thing`` 키에 해당하는 값은 두 번째 오브젝트의 `thing: 'bar'`의 값을 가져오므로 `'bar'`를 결과 오브젝트에 포함하고, `values` 키에 해당하는 값은 `R.concat([10, 20], [15, 35])`이 된 값을 반환하므로 `[10, 20, 15, 35]` 값을 결과 오브젝트에 포함하게 된다.
- 또한 두 오브젝트를 합치는 merge 이므로 `a: true`와 `b: true`는 주어진 함수를 사용하는 것은 아니지만 결과 오브젝트에 포함이 되면서 `{ a: true, b: true, thing: 'bar', values: [10, 20, 15, 35] }`라는 값이 된다.

## Reference
- https://ramdajs.com/docs/#mergeWithKey
