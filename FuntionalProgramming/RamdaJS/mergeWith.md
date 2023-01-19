## mergeWith
> Creates a new object with the own properties of the two provided objects. 
- 주어진 두 오브젝트가 가진 모든 프로퍼티를 가진 새로운 오브젝트를 생성한다.
> If a key exists in both objects, the provided function is applied to the values associated with the key in each object, with the result being used as the value associated with the key in the returned object.
- 만약 주어진 오브젝트 모두에 동일한 키가 있다면, 제공된 함수에 두 오브젝트의 키에 할당된 값이 적용되며, 함수에 적용된 결과값은 반횐되는 오브젝트 키에 할당되어 사용된다.

> See also mergeDeepWith, merge, mergeWithKey.

## 설명
- 두 오브젝트를 받아 각각의 오브젝트가 가진 프로퍼티를 모두 합친 새로운 객체를 반환하며, 두 오브젝트의 키가 중복된다면 중복되는 동일한 키에 할당된 값을 주어진 함수의 인자로 전달하여 평가된 결과 값을 반환되는 오브젝트의 키에 할당한 오브젝트를 반환환다.

## 표현
```
((a, a) → a) → {a} → {a} → {a}
```
- `((a, a) → a) →` 첫 번째 인자로 함수를 받는다. 두 번째 세 번째 인자로 오는 오브젝트가 가진 프로퍼티의 벨류로 지정될 수 있는 종류의 값이 되어야 한다.
- `→ {a} →` 두 번째 인자로 오브젝트를 받는다.
- `→ {a} →` 세 번째 인자로 오브젝트를 받는다.
- `→ {a}` 새로운 오브젝트를 반환한다. 이 때 두 번째와 세 번째로 받은 인자의 키가 동일할 때 두 오브젝트의 해당 키의 값을 첫 번째 함수의 인자로 넣으며 이 때 첫 번째 함수는 해당 값의 타입을 받을 수 있어야 한다.


## 예제
```
R.mergeWith(R.concat,
            { a: true, values: [10, 20] },
            { b: true, values: [15, 35] });
//=> { a: true, b: true, values: [10, 20, 15, 35] }
```
- 두 오브젝트의 키 `a`와 `b`는 한쪽의 오브젝트에만 존재한다. 따라서 두 키를 합쳐도 중복이 되지 않으므로 반환되는 오브젝트에 모두 포함된다.
- 하지만 `value`는 동일한 키이다. 따라서 키의 값을 함수에 전달해야 한다. 따라서 반환되는 오브젝트의 `value` 값은 `R.concat([10, 20], [15, 35])`로 `[10, 20, 15, 35]`가 된다.
- 따라서 결과는 키 `a`와 그 값, 키 `b`와 그 값, 키 `value`와 함수에 의해 반환된 값으로 구성된 오브젝트 `{ a: true, b: true, values: [10, 20, 15, 35] }`가 된다.

## Reference
- https://ramdajs.com/docs/#mergeWith
