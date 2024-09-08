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

## References
- https://ramdajs.com/docs/#whereAny
