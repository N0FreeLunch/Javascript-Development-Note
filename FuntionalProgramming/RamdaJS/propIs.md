## propIs
> Returns true if the specified object property is of the given type; false otherwise.
- 지정한 오브젝트의 프로퍼티가 주어진 타입에 해당할 때 true를 반환하고 그렇지 않으면 false를 반환한다.

> See also is, propSatisfies.

### 설명
- 오브젝트의 지정한 프로퍼티의 값의 타입이 주어진 타입과 일치하는지 확인한다.
- 이 때 타입은 자바스크립트 네티이브 기능인 타입 오브젝트를 받는다. 타입 오브젝트는 생성자로 인자를 할당할 경우에는 할당된 값을 지정한 타입으로 형 변환을 하며, 오브젝트로 쓰일 경우에는 수 타입을 다루기 위한 여러 메소드들을 제공한다. 확인할 타입을 지정할 때는 생성자를 실행하지 않은 상태의 타입 오브젝트를 사용한다.
- 찻 반쩨 인자로 타입을 받는다.
- 두 번째 인자로 선택할 프로퍼티를 받는다.
- 세 번째 인자로 대상 오브젝트를 받는다.
- 네이티브 타입 오브젝트와 대상 오브젝트의 지정한 프로퍼티의 값의 타입이 일치하는지 확인한다.

### 표현
```
Type → String → Object → Boolean
```
- `Type →`: 첫 번째 인자로 타입을 받는다. 자바스크립트 네이티브 오브젝트에 해당하는 타입 오브젝트를 받으며, String, Number, Array 등이 존재한다.
- `→ String →`: 두 번째 인자로 오브젝트의 프로퍼티를 선택하기 위한 값을 받는다.
- `→ Object →`: 세 번째 인자로 대상 오브젝트를 받는다.
- `→ Boolean`: 오브젝트의 지정한 프로퍼티의 값이 첫 번째 인자로 받은 타입과 일치하면 true, 아니면 false를 반환한다.

### 예제
```js
R.propIs(Number, 'x', {x: 1, y: 2});  //=> true
R.propIs(Number, 'x', {x: 'foo'});    //=> false
R.propIs(Number, 'x', {});            //=> false
```
- `{x: 1, y: 2}`에서 `'x'` 프로퍼티의 값은 1이며 `Number` 타입과 일치하므로 true이다.
- `{x: 'foo'}`에서 `x` 프로퍼티의 값은 `'foo'`이며 문자열이므로 `Number` 타입과 일치하지 않으므로 false이다.
- `{}` 빈 배열에서 `'x'` 프로퍼티는 존재하지 않으므로 `prop`의 결과는 `undefined`이다. `undefined`는 `Number` 타입과 일치하지 않으므로 false이다.

## Reference
- https://ramdajs.com/docs/#propIs

