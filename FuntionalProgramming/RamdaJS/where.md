## where
> Takes a spec object and a test object; returns true if the test satisfies the spec.
- 스펙 오브젝트와 테스트 오브젝트를 받는다. 만약 테스트 (오브젝트)가 스펙을 만족하면 true를 반환한다.
> Each of the spec's own properties must be a predicate function.
- 스펙이 가진 각 프로퍼티들는 술어함수여야 한다.
> Each predicate is applied to the value of the corresponding property of the test object.
- 각각의 술어는 테스트 오브젝트의 일치하는 프로퍼티의 값에 적용된다.
> where returns true if all the predicates return true, false otherwise.
- where (함수는) 만약 모든 술어(스펙 오브젝트)가 true를 반환할 때 true를 반환한다.

> where is well suited to declaratively expressing constraints for other functions such as filter and find.
- where은 filter나 find와 같은 다른 함수들에 대한 선언적 표현의 제약 사항을 나타내는데 아주 적합하다.

> See also propSatisfies, whereEq.

### 설명
- 오브젝트의 각 프로퍼티가 지정한 조건을 만족하는지 확인하는 스펙 오브젝트를 통해, 테스트 대상이 되는 다른 오브젝트가 스펙 오브젝트를 만족하는지 확인한다.
- 스펙 오브젝트는 각 프로퍼티의 값으로 술어함수를 가지며, 테스트 대상이 되는 오브젝트의 각 프로퍼티 중에 스펙 오브젝트의 프로퍼티에 해당하는 프로퍼티가 있다면 테스트 오브젝트의 동일 프로퍼티의 값은 스펙 오브젝트의 술어함수에 전달되어 술어함수를 만족하는지 판별한다. 테스트 오브젝트가 스펙 오브젝트의 모든 술어함수를 만족한다면 where 함수는 true를 반환하고 그렇지 않으면 false를 반환한다.

### 표현
```
{String: (* → Boolean)} → {String: *} → Boolean
```
- `{String: (* → Boolean)} →`: 첫 번째 인자로는 오브젝트를 받는데, 스펙 오브젝트로 불린다. 이 오브젝트는 문자열의 프로퍼티를 가지고 프로퍼티가 술어함수를 가져야 한다. 인자로는 아무거나(`*`) 전달될 수 있는데
- `→ {String: *} →`: 두 번째 인자 또는 첫 번째 인자를 전달한 반환값 함수의 인자로 오브젝트를 받는데, 테스트 오브젝트라고 불린다. 이 오브젝트가 가진 프로퍼티의 값은 스펙 오브젝트의 동일 프로퍼티의 술어 함수에 전달되어 술어함수를 만족하는지 판단한다.
- `→ Boolean`: 테스트 오브젝트의 프로퍼티 값 각각에 매칭되는 스펙 오브젝트의 프로퍼티의 술어함수를 모두 true로 만족하면 true를 반환한다.

### 예제
```js
// pred :: Object -> Boolean
const pred = R.where({
  a: R.equals('foo'),
  b: R.complement(R.equals('bar')),
  x: R.gt(R.__, 10),
  y: R.lt(R.__, 20)
});

pred({a: 'foo', b: 'xxx', x: 11, y: 19}); //=> true
pred({a: 'xxx', b: 'xxx', x: 11, y: 19}); //=> false
pred({a: 'foo', b: 'bar', x: 11, y: 19}); //=> false
pred({a: 'foo', b: 'xxx', x: 10, y: 19}); //=> false
pred({a: 'foo', b: 'xxx', x: 11, y: 20}); //=> false
```
- `{a: R.equals('foo'), b: R.complement(R.equals('bar')), x: R.gt(R.__, 10), y: R.lt(R.__, 20)}`는 스펙 오브젝트에 해당한다. 그리고 where 함수의 반환 함수의 인자로 넣는 `{a: 'foo', b: 'xxx', x: 11, y: 19}`, `{a: 'xxx', b: 'xxx', x: 11, y: 19}`, `{a: 'foo', b: 'bar', x: 11, y: 19}`, `{a: 'foo', b: 'bar', x: 11, y: 19}`, `{a: 'foo', b: 'xxx', x: 10, y: 19}`, `{a: 'foo', b: 'xxx', x: 11, y: 20}`는 테스트 오브젝트에 해당한다.
- 테스트 오브젝트는 프로퍼티 a, b, x, y를 가지고 있으며, 스펙 오브젝트도 프로퍼티 a, b, x, y를 가지고 있다. 스펙 오브젝트의 프로퍼티는 `R.equals('foo')`, `R.complement(R.equals('bar'))`, `R.gt(R.__, 10)`, `R.lt(R.__, 20)`의 술어 함수를 가지고 있으며, 테스트 오브젝트의 프로퍼티 각각의 값은 일치하는 스펙 프로퍼티의 술어함수에 전달되어 술어함수를 만족하는지 판별한다.
- 모든 스펙 오브젝트의 프로퍼티의 술어함수를 만족하면 `where` 함수에 의해 반환된 `pred` 함수는 true를 반환하고 그렇지 않으면 false를 반환한다.
- `{a: 'foo', b: 'xxx', x: 11, y: 19}`는 스펙 오브젝트를 만족하므로 true를 반환하며, `{a: 'xxx', b: 'xxx', x: 11, y: 19}`는 `R.equals('foo')`를 만족하지 않으므로 false를 반환하며, `{a: 'foo', b: 'bar', x: 11, y: 19}`는 `R.complement(R.equals('bar'))`에 따라 `'bar'`가 아니어야 하는데 `'bar'`라서 false를 반환하며, `{a: 'foo', b: 'xxx', x: 10, y: 19})`는 `R.gt(R.__, 10)`에 의해 10 보타 커야 하는데 10이라서 만족하지 않으므로 false를 반환하며, `{a: 'foo', b: 'xxx', x: 11, y: 20}`는 `R.lt(R.__, 20)`에 의해 20 보다 작아야 하는데 20이라서 만족하지 않으므로 false를 반환한다.

## References
- https://ramdajs.com/docs/#where
