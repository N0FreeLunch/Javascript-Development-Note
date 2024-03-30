## partition
> Takes a predicate and a list or other Filterable object and returns the pair of filterable objects of the same type of elements which do and do not satisfy, the predicate, respectively. Filterable objects include plain objects or any object that has a filter method such as Array.
- 술어함수와 리스트 또는 여타 필터링 가능한 개체를 받아, 동일한 타입의 원소로 구성된 필터링 가능한 객체들의 한 쌍을 반환한다. (배열 안에 술어 함수에 의해 분류된 두 리스트가 있으며 각 리스트는 필터링 가능하다. 리스트는 배열 또는 오브젝트가 될 수 있다.) 이 때, 각 배열의 각각의 원소는 주어진 술어함수를 충족하거나 하지 않는지를 판별할 수 있는 원소로 구성되어 있어야 한다. 필터링 가능한 오브젝트는 plain 오브젝트 또는 배열과 같은 오브젝트의 filter 메소드를 갖는 오브젝트에 해당한다.

> See also filter, reject.

### 설명
- 첫 번째 인자로 술어 함수를 받고, 두 번째 인자로는 술어 함수에 의해 참, 거짓의 판단이 가능한 리스트를 받는다. 이 때 리스트는 필러링 가능한 대상으로, 배열, 플레인 오브젝트 등에 해당한다.
- 술어 함수를 통과하는 원소 리스트와 술어 함수를 통과하지 않는 원소 리스트를 배열 형식으로 반환하며, 리스트는 두 번째 인자로 받은 리스트의 형식을 따른다. 두 번째 인자로 받은 리스트가 배열이면 `[[참이 되는 원소 리스트], [거짓이 되는 원소 리스트]]`으로 배열인 리스트를 두 개 반환하고, 오브젝트이면 `[{참이 되는 원소 리스트}, {거짓이 되는 원소 리스트}]`를 반환한다.

### 표현
```
Filterable f => (a → Boolean) → f a → [f a, f a]
```
- `Filterable f =>` 필터링 가능한 리스트 f에 대해
- `(a → Boolean) →` 첫 번째 인자로 리스트의 원소를 판별할 술어 함수를 받는다.
- `→ f a →` 두 번째 인자로 리스트 f에 a 타입의 원소를 받는다.
- `→ [f a, f a]` 두 번째 인자로 받은 리스트와 동일한 종류의 리스트로 동일한 타입의 a 원소를 갖는 `f a` 리스트를 배열 안에 두 리스트로 담아 반환한다.

### 예제
```js
R.partition(R.includes('s'), ['sss', 'ttt', 'foo', 'bars']);
// => [ [ 'sss', 'bars' ],  [ 'ttt', 'foo' ] ]

R.partition(R.includes('s'), { a: 'sss', b: 'ttt', foo: 'bars' });
// => [ { a: 'sss', foo: 'bars' }, { b: 'ttt' }  ]
```

#### 배열 리스트의 경우
- 문자열에 s라는 케릭터가 들어가 있는지 판별하는 술어 함수인 `R.includes('s')`을 받고, 술어 함수에 의해 필터 가능한 원소를 갖는 리스트인 `['sss', 'ttt', 'foo', 'bars']`를 받았다. 리스트의 각 원소를 술어 함수에 대입했을 때 참이 되는 것은 반환 배열의 첫 번째 배열에 포함하여 `[ 'sss', 'bars' ]`가 되고, 거짓이 되는 것은 반환 배열의 두 번째 배열에 포함되어 `[ 'ttt', 'foo' ]`가 된다.

#### 오브젝트 리스트의 경우
- 배열의 경우와 마찬가지이지만, 리스트로 배열이 아닌 오브젝트를 받고, 키에 대응하는 벨류가 술어함수에 의해 필터링 가능한 문자열인 값으로 받았다. 반환된 값은 `[[참이 된 원소 리스트], [거짓이 되는 원소 리스트]]`가 아닌 `[{참이 된 원소 리스트}, {거짓이 된 원소 리스트}]`가 된다.

## Reference
- https://ramdajs.com/docs/#partition
