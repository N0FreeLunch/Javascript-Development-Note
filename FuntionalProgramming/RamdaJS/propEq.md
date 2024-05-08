## propEq
> Returns true if the specified object property is equal, in R.equals terms, to the given value; false otherwise. You can test multiple properties with R.whereEq, and test nested path property with R.pathEq.
- 주어진 값이 지정한 오브젝트 프로퍼티와 일치하면 true를 반환한다. 이 때 내부적으로 일치의 판단은 R.equals를 사용하며 일치하지 않으면 false를 반환한다. R.whereEq을 사용해서 복수의 프로퍼티의 일치도 테스트 할 수 있으며, R.pathEq를 사용하여 중접된 경로의 속성을 테스트 할 수 있다.

> See also whereEq, pathEq, propSatisfies, equals.

### 설명
- 일치를 확인할 값, 대상 프로퍼티, 대상 오브젝트 3가지 인자를 받아 대상 오브젝트의 지정한 프로퍼티의 값이 확인할 값과 동일하면 참 아니면 거짓을 반환하는 술어함수이다.
- 일치를 확인할 값과 대상 프로퍼티를 커링을 통해 미리 머금은 오브젝트 리스트를 필터링 하는 술어함수로 사용할 때 적절하다.
- 첫 번째 인자로 일치를 확인할 값을 받는다.
- 두 번째 인자로 오브젝트에서 접근할 프로퍼티를 받는다.
- 세 번째 인자로 대상 오브젝트를 받는다.

### 표현
```
a → String → Object → Boolean
```
- `a →`: 첫 번째 인자로 일치하는지 확인하기 위한 값을 하나 받는다.
- `→ String →`: 두 번째 인자로 값을 취득하기 위한 오브젝트의 프로퍼티를 받는다.
- `→ Object →`: 세 번째 인자로 대상 오브젝트를 전달 받는다.
- `→ Boolean`: 세 번째 인자로 받은 오브젝트에서 두 번째 인자로 지정한 프로퍼티 값이 존재할 때 그 값이 첫 번째로 받은 인자와 같다면 true, 아니면 false를 반환한다.

### 예시
```js
const abby = {name: 'Abby', age: 7, hair: 'blond'};
const fred = {name: 'Fred', age: 12, hair: 'brown'};
const rusty = {name: 'Rusty', age: 10, hair: 'brown'};
const alois = {name: 'Alois', age: 15, disposition: 'surly'};
const kids = [abby, fred, rusty, alois];
const hasBrownHair = R.propEq('brown', 'hair');
R.filter(hasBrownHair, kids); //=> [fred, rusty]
```
- `kids`는 변수에 아이들(kids)의 이름을, name, age, hair 프로퍼티를 갖는 키를 가진 오브젝트를 원소로 한 리스트(배열)로 구성되어 있다.
- `R.propEq('brown', 'hair')`는 오브젝트를 하나 더 인자로 받아 오브젝트의 `'hair'` 프로퍼티에 대응하는 값이 `'brown'`과 일치하는지 확인한다.
- `R.filter(hasBrownHair, kids)`은 `R.filter(function (obj) { ... }, [abby, fred, rusty, alois])`의 형식으로 바꿀 수 있고, 오브젝트를 원소로 하는 배열을 받고, 콜백함수는 배열의 원소인 각각의 오브젝트를 하나씩 전달 받아 참 거짓을 반환하는 술어함수임을 알 수 있다. `hasBrownHair`는 오브젝트를 받아서 `'hair'` 프로퍼티에 대응하는 값이 `'brown'`과 일치하는지 확인하는 함수이므로 콜백함수의 위치에 넣어도 된다. `kids` 배열에서 `hasBrownHair`를 만족하는 대상만을 필터하므로 `hair` 속성이 `'brown'`인 fred, rusty가 뽑혔다.

## Reference
- https://ramdajs.com/docs/#propEq
