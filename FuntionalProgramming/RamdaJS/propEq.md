## propEq
> Returns true if the specified object property is equal, in R.equals terms, to the given value; false otherwise. You can test multiple properties with R.whereEq, and test nested path property with R.pathEq.
- 주어진 값이 지정한 오브젝트 프로퍼티와 일치하면 true를 반환한다. 이 때 내부적으로 일치의 판단은 R.equals를 사용하며 일치하지 않으면 false를 반환한다. R.whereEq을 사용해서 복수의 프로퍼티의 일치도 테스트 할 수 있으며, R.pathEq를 사용하여 중접된 경로의 속성을 테스트 할 수 있다.

> See also whereEq, pathEq, propSatisfies, equals.

### 설명


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

## Reference
- https://ramdajs.com/docs/#propEq
