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

### 표현
```
{String: (* → Boolean)} → {String: *} → Boolean
```

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

## References
- https://ramdajs.com/docs/#where
