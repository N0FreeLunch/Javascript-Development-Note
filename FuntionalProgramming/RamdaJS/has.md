## has
> Returns whether or not an object has an own property with the specified name

## 표현
```
s → {s: x} → Boolean
```
- `s →` 첫 번째 인자로 두 번재 인자로 들어오는 오브젝트의 프로퍼티명으로 가능한 종류의 인자를 받는다. `s`는 문자열 형태의 값을 받는다는 의미이다.
- `→ {s: x} →` 두 번째 인자로 오브젝트를 받는다.
- `→ Boolean` 지정한 프로퍼티 명이 주어진 오브젝트에 존재하면 참 아니면 거짓을 반환한다.

## 설명
- 첫 번째 인자로 프로퍼티명을 받는다.
- 두 번째 인자로 오브젝트를 받는다.
- 주어진 오브젝트에서 지정한 이름의 프로퍼티명을 가지고 있다면 참을 반환 아니면 거짓을 반환한다.

## 예제
```
const hasName = R.has('name');
hasName({name: 'alice'});   //=> true
hasName({name: 'bob'});     //=> true
hasName({});                //=> false

const point = {x: 0, y: 0};
const pointHas = R.has(R.__, point);
pointHas('x');  //=> true
pointHas('y');  //=> true
pointHas('z');  //=> false
```
- `R.has('name')`으로 오브젝트를 인자로 받아서 `name` 프로퍼티가 존재하면 참을 반환하고 그렇지 않으면 거짓을 반환하는 함수이다.
- `{name: 'alice'}`, `{name: 'bob'}`는 `name` 프로퍼티를 가지고 있으므로 참을 반환하고, `{}`는 `name` 프로퍼티를 가지지 않으므로 거짓을 반환한다.
- `R.has(R.__, point)`는 첫 번째 인자는 평가된 함수(`pointHas`)의 인자로 받고 두 번째 인자를 미리 `{x: 0, y: 0}`으로 지정한다.
- `{x: 0, y: 0}` 오브젝트에서 x 프로퍼티명이 있으므로 true, y 프로퍼티명이 있으므로 false, z 프로퍼티명이 없으므로 false이다.

## Reference
- https://ramdajs.com/docs/#has
