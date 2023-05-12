## modify
> Creates a copy of the passed object by applying an fn function to the given prop property.
- `modify` 함수는 인자로 오브젝트를 받고, 받은 오브젝트에서 주어진 프로퍼티의 이름에 해당하는 대상의 값을 변경한다. 값의 변경을 위해서 지정된 프로퍼티의 값을 인자로 전달 받으면 평가되어 반환하는 함수 `fn`을 인자로 받고 주어진 오브젝트에서 대상 프로퍼티의 값이 `fn`을 통해 바뀌게 된 오브젝트를 복사본으로 반환한다.
> The function will not be invoked, and the object will not change if its corresponding property does not exist in the object. All non-primitive properties are copied to the new object by reference.

## 설명

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
