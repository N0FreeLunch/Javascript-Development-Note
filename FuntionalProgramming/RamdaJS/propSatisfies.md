## propSatisfies
> Returns true if the specified object property satisfies the given predicate; false otherwise. You can test multiple properties with R.where.
- 주어진 술어함수를 만족하는 오브젝트의 프로퍼티가 지정되면, true를 반환한다. 만약 조건을 만족하지 못하면 false를 반환한다. `R.where`와 함께 쓰여 복수의 프로퍼티를 테스트 할 수 있다.

> See also where, propEq, propIs.

### 설명
- 지정한 프로퍼티의 값이 주어진 술어함술르 만족하면 true, 아니면 false를 반환한다. 대상 프로퍼티가 존재하지 않는 경우에는 그렇지 않은 경우에 해당하므로 false가 반환된다.
- `propSatisfies`가 하나의 프로퍼티의 값에 대한 참 거짓을 판별하는 반면, `where`은 오브젝트가 가진 각각의 프로퍼티에 대한 술어함수를 지정해서 여러 프로퍼티에 대해 각 값이 술어함수를 만족하는지 확인하는 함수이다.

### 표현
```
(a → Boolean) → String → {String: a} → Boolean
```
- `(a → Boolean) →`: 첫 번째 인자로 술어 함수를 받는다.
- `→ String →`: 두 번째 인자로 대상 프로퍼티를 지정한다.
- `→ {String: a} → `: 세 번째 인자로 대상 오브젝트를 지정한다. 오브젝트의 키는 두 번째 인자로 받는 대상의 타입과 일치하는 String, 오브젝트의 값은 술어함수의 인자로 들어갈 수 있는 종류인 a가 된다.
- `→ Boolean`: 프로퍼티의 값이 주어진 술어함수를 만족하면 true 아니면 false를 반환한다.

### 예제
```js
R.propSatisfies(x => x > 0, 'x', {x: 1, y: 2}); //=> true
```
- `{x: 1, y: 2}` 오브젝트에서 `'x'`라는 프로퍼티를 뽑았을 때 1이란 값을 갖는다. 주어진 술어함수 `x => x > 0`에 1을 전달했을 때, true가 되므로 true를 반환한다.

### Reference
- https://ramdajs.com/docs/#propSatisfies
