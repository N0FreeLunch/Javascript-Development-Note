## modify
> Creates a copy of the passed object by applying an fn function to the given prop property.
- 인자로 전달된 오브젝트의 복사본을 만든다. 이 때 반환되는 오브젝트는 `fn` 함수에 지정한 프로퍼티 이름에 해당하는 프로퍼티 값을 전달하여 적용된 값으로 대체된다.
> The function will not be invoked, and the object will not change if its corresponding property does not exist in the object. All non-primitive properties are copied to the new object by reference.
- 만약 일치하는 프로퍼티가 오브젝트에 존재하지 않으면 주어진 `fn` 함수를 실행하지 않는다. 이에 따라 반환되는 오브젝트도 변경되지 않으며, 반환되는 오브젝트는 복사가 아닌 새로운 오브젝트를 반환하지만, 비-원시타입에 해당하는 값을 갖는 프로퍼티들은 모두 참조 방식으로 복사된다.

#### fn이란?
- `fn`은 함수를 반환하는 함수를 의미한다. 함수의 인자로 할당된 함수는 전달되는 함수 내부에서 인자를 받아서 평가될 필요가 있다. 인자를 받아서 평가되기 위해서는 함수가 아직 평가에 이르지 않았다는 의미이다. 함수가 평가된다는 말은 받아야 할 인자를 모두 받아서 함수가 반환하고자하는 최종 목적의 값에 이르렀다는 의미를 가진다. 커링에 의해서 함수의 인자 최종적인 결과값을 얻기에 충분한 인자를 획득하지 못한 경우나 아직 인자를 아무것도 받지 못한 경우의 함수를 `fn`이라고 부른다.

## 설명
- `modify` 함수는 인자로 변경할 프로퍼티, 프로퍼티의 값에 적용할 함수(`fn`), 오브젝트를 순차적으로 받아서 지정한 프로퍼티명에 해당하는 프로퍼티의 값을 `fn` 함수에 전달하여 얻은 결과값으로 해당 프로퍼티의 값을 대체한 오브젝트를 반환한다. 이 때 반환되는 오브젝트는 복사본의 오브젝트이다.

## 표현
```
Idx → (v → v) → {k: v} → {k: v}
```

## 예제
```js
const person = {name: 'James', age: 20, pets: ['dog', 'cat']};
R.modify('age', R.add(1), person); //=> {name: 'James', age: 21, pets: ['dog', 'cat']}
R.modify('pets', R.append('turtle'), person); //=> {name: 'James', age: 20, pets: ['dog', 'cat', 'turtle']}
```

## Reference
- https://ramdajs.com/docs/#modify
