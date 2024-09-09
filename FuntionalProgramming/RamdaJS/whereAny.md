## whereAny
> Takes a spec object and a test object; each of the spec's own properties must be a predicate function.
- 스펙 오브젝트와 테스트 오브젝트를 받아서, 스펙이 가진 각각의 프로퍼티는 반드시 술어 함수여야 한다.
> Each predicate is applied to the value of the corresponding property of the test object.
- 각각의 술어는 테스트 오브젝트의 일치하는 프로퍼티의 값에 적용된다.
> whereAny returns true if at least one of the predicates return true, false otherwise.
- 술어함수 중 적어도 하나가 true를 반환하면 whereAny는 true를 반환하고 그렇지 않으면 false를 반환한다.
> whereAny is well suited to declaratively expressing constraints for other functions such as filter and find.
- whereAny는 filter나 find와 같은 다른 함수의 제약을 선언적으로 표현하는데 적합하다.

> See also propSatisfies, where.

### 설명

### 표현
```
{String: (* → Boolean)} → {String: *} → Boolean
```
- `{String: (* → Boolean)} →`: 첫 번째 인자로는 오브젝트를 받는데, 스펙 오브젝트로 불린다. 이 오브젝트는 문자열의 프로퍼티를 가지고 프로퍼티가 술어함수를 가져야 한다. 인자로는 아무거나(`*`) 전달될 수 있는데
- `→ {String: *} →`: 두 번째 인자 또는 첫 번째 인자를 전달한 반환값 함수의 인자로 오브젝트를 받는데, 테스트 오브젝트라고 불린다. 이 오브젝트가 가진 프로퍼티의 값은 스펙 오브젝트의 동일 프로퍼티의 술어 함수에 전달되어 술어함수를 만족하는지 판단한다.
- `→ Boolean`: 테스트 오브젝트의 프로퍼티 값 각각에 매칭되는 스펙 오브젝트의 프로퍼티의 술어함수를 적어도 하나를 true로 만족하면 true를 반환한다.


### 예제
```
// pred :: Object -> Boolean
const pred = R.whereAny({
  a: R.equals('foo'),
  b: R.complement(R.equals('xxx')),
  x: R.gt(R.__, 10),
  y: R.lt(R.__, 20)
});

pred({a: 'foo', b: 'xxx', x: 8, y: 34}); //=> true
pred({a: 'xxx', b: 'xxx', x: 9, y: 21}); //=> false
pred({a: 'bar', b: 'xxx', x: 10, y: 20}); //=> false
pred({a: 'foo', b: 'bar', x: 10, y: 20}); //=> true
pred({a: 'foo', b: 'xxx', x: 11, y: 20}); //=> true
```
- `{ a: R.equals('foo'), b: R.complement(R.equals('xxx')), x: R.gt(R.__, 10), y: R.lt(R.__, 20) }`는 스펙 오브젝트에 해당한다. whereAny는 스펙 오브젝트의 각 프로퍼티의 술어함수 중 하나만 만족해도 true를 반환한다.
- `{a: 'foo', b: 'xxx', x: 8, y: 34}`, `{a: 'xxx', b: 'xxx', x: 9, y: 21}`, `{a: 'bar', b: 'xxx', x: 10, y: 20}`, `{a: 'foo', b: 'bar', x: 10, y: 20}`, `{a: 'foo', b: 'xxx', x: 11, y: 20}`는 테스트 오브젝트에 해당한다. 각각이 스펙 오브젝트를 만족하는지 살펴보자.
- `{a: 'foo', b: 'xxx', x: 8, y: 34}`는 `a: 'foo'`가 술어함수 `a: R.equals('foo')`를 만족하므로 true가 된다. `{a: 'xxx', b: 'xxx', x: 9, y: 21}`는 만족하는 술어함수가 하나도 없으므로 false가 된다. `{a: 'bar', b: 'xxx', x: 10, y: 20}`도 만족하는 술어함수가 하나도 없으므로 false가 된다. `{a: 'foo', b: 'bar', x: 10, y: 20}`는 `a: R.equals('foo')`를 만족하므로 true가 된다. `{a: 'foo', b: 'xxx', x: 11, y: 20}`는 `a: R.equals('foo')`를 만족하므로 true가 된다.

## References
- https://ramdajs.com/docs/#whereAny
