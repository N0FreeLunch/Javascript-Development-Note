## clone

> Creates a deep copy of the source that can be used in place of the source object without retaining any references to it. 
- 깊은 복사가 된 대상을 만들어 낸다. 깊은 복사가 된 객체는 원본 객체가 가진 어떠한 참조도 유지하지(retaining) 않으며 각 참조 또한 복사된다. 깊은 복사 된 객체는 원본 객체 대신에 사용할 수 있다.
> The source object may contain (nested) Arrays and Objects, Numbers, Strings, Booleans and Dates.
- (깊은 복사의 대상이 되는) 원본 객체는 배열, 객체, 수, 문자열, 불리언, 날짜 등을 객체 내부에 포함하고 있고 중첩된 방식으로도 이들을 가질 수도 있다.
> Functions are assigned by reference rather than copied.
- 함수는 복사되기 보다는 참조로 할당된다.
> Dispatches to a clone method if present.
- 복사가 될 원본 대상이 존재하면 `clone`메소드는 디스패치된다.
> Note that if the source object has multiple nodes that share a reference, the returned object will have the same structure, but the references will be pointed to the location within the cloned value.
- 만약 원본 객체가 다수의 참조를 공유하는 노드(객체 내부의 멤버와 같은 대상을 말함. 노드라고 표현한 것은 대상이 다른 대상을 또한 포함할 수 있는 중첩된 구조를 가질 수 있기 때문)를 가지고 있는 경우, 깊은 복사된 값은 원본 소스와 동일한 구조를 가지지만 참조하는 대상은 원본의 참조값을 가리키는 것이 아닌 복사된 값 내부 위치를 가리킨다.

### 설명
- 자바스크립트에서 거의 모든 값은 객체에 해당한다. 오브젝트 뿐만 아니라, 배열, 객체, 문자열, 수, 불리언, 날짜 모두 원시 타입을 가지고 있지만 필요에 따라 객체로 자동 형변환 되는 대상들이다.
- 자바스크립트의 객체로 표현될 수 있는 대상의 깊은 복사 값을 만드는 함수이다.
- 깊은 복사란 객체가 일반적으로 멤버로 가지고 있거나 중첩되어 포함하고 있는 값들에 대해 값이 참조를 하는 경우 참조 값의 원본을 그대로 가리키는 것이 아닌 복사본을 만들어 참조하는 방식으로 복제본을 만드는 것이다.

### 문법
```
R.clone(value): *
```
> `value`: The object or array to clone
- `value`: 복사할 오브젝트 또는 배열
> Returns * A deeply cloned copy of `val`
- (*) `val` 깊은 복사가 된 값을 반환한다. 이 값은 특별한 타입 제한이 없다.

### 표현
```
{*} → {*}
```
- `{*} →` 임의의 형태의 오브젝트를 인자로 받아서
- `→ {*}` 깊은 복사 된 대상을 반환한다.

### 예제
```js
const objects = [{}, {}, {}];
const objectsClone = R.clone(objects);
objects === objectsClone; //=> false
objects[0] === objectsClone[0]; //=> false
```
- `const objects = [{}, {}, {}];` 원본 소스를 `[{}, {}, {}]`이라고 하자.
- `const objectsClone = R.clone(objects)` 깊은 복사된 대상을 `objectsClone`이라고 하자.
- `objects === objectsClone` 두 객체가 동일한지 확인하더라도 `false`를 반환하므로 서로 다른 객체이다.
- `objects[0] === objectsClone[0]` 두 객체의 참조 대상인 배열의 첫 번째 오브잭트 `{}` 또한 복사가 되었기 때문에 두 객체는 일치하지 않는다. 따라서 `false`를 반환한다.

### References
- https://ramdajs.com/docs/#clone
- https://github.com/ramda/ramda/blob/master/test/clone.js
- https://github.com/ramda/types/blob/develop/types/clone.d.ts
