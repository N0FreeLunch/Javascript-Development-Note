## filter
> Takes a predicate and a Filterable, and returns a new filterable of the same type containing the members of the given filterable which satisfy the given predicate. Filterable objects include plain objects or any object that has a filter method such as Array.

> Dispatches to the filter method of the second argument, if present.

> Acts as a transducer if a transformer is given in list position.


## 표현
```
Filterable f => (a → Boolean) → f a → f a
```
- `Filterable f =>` f는 필터 기능을 적용할 수 있는 대상이다.
- `(a → Boolean) →` 첫 번째 인자로는 술어함수를 받는다.
- ` → f a →` 두 번째 인자로는 필터 기능을 적용할 수 있는 인자(배열 또는 오브젝트)를 받는다.
- `→ f a` 두 번째 인자로 받은 배열과 동일한 필터 기능을 적용할 수 있는 형태로 반환한다.

## 설명
- 주어진 리스트(배열 또는 오브젝트)를 순회하면서 주어진 술어함수를 만족하는 원소 또는 프로퍼티만 뽑아내어 반환한다.

## 예제
```
const isEven = n => n % 2 === 0;

R.filter(isEven, [1, 2, 3, 4]); //=> [2, 4]

R.filter(isEven, {a: 1, b: 2, c: 3, d: 4}); //=> {b: 2, d: 4}
```
- `1, 2, 3, 4`에서 짝수인 것은 `2, 4` 이고 주어진 대상이 배열이므로 `[2, 4]`를 반환한다.
- `a: 1, b: 2, c: 3, d: 4`에서 프로퍼티의 벨류가 짝수인 프로퍼티는 `b: 2, d: 4`이고 주어진 대상이 오브젝트이므로 `{b: 2, d: 4}`를 반환한다.


## Reference
- https://ramdajs.com/docs/#filter
