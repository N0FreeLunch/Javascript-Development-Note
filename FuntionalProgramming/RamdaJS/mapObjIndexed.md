## mapObjIndexed
> An Object-specific version of map. 
- 어떤 특별한 유형의 오브젝트에 적용할 수 있는 버전의 map함수이다.

> The function is applied to three arguments: (value, key, obj).
- 사용되는 함수는 value, key, obj의 3가지 인자의 적용을 받는다.

> If only the value is significant, use map instead.
- 키나 오브젝트의 영향이나 변화 없이 값만 변경되는 경우 map 함수를 대신 사용한다.

## 설명
- 오브젝트의 키를 순회하여 키에 대응하는 벨류의 값을 주어진 함수로 바꾼 결과를 표현한다.

## 표현
```
((*, String, Object) → *) → Object → Object
```
- `((*, String, Object) → *)` 첫 번째 인자로 함수를 받는다. 이 함수는 콜백 함수로 `(*, String, Object)`의 인자를 받아서 값, 키, 오브젝트의 속성을 이용하여 벨류의 변경을 정의할 수 있게 한다.
- `→ Object →` 두 번째 인자로는 오브젝트를 받는다. mapObjIndexed 함수는 이 오브젝트의 키를 차례로 순회한다.
- `→ Object` 두 번째 인자로 주어진 오브젝트와 동일한 키를 가진 벨류만 바뀐 오브젝트를 반환한다.

## 예제
```
const xyz = { x: 1, y: 2, z: 3 };
const prependKeyAndDouble = (num, key, obj) => key + (num * 2);

R.mapObjIndexed(prependKeyAndDouble, xyz); //=> { x: 'x2', y: 'y4', z: 'z6' }
```

## Reference
- https://ramdajs.com/docs/#mapObjIndexed
