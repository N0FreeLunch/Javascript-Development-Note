## prop
> Returns a function that when supplied an object returns the indicated property of that object, if it exists.
- 오브젝트가 주어졌을 때 오브젝트의 지정한 프로퍼티를 반환하는 함수를 반환한다. 이 때 지정한 프로퍼티가 오브젝트에 존재해야 한다.

> See also path, props, pluck, project, nth.

## 설명
- 프로퍼티 하나를 지정하고 오브젝트를 하나 받아서 오브젝트에서 지정한 프로퍼티에 해당하는 값을 뽑아낸다. 지정한 프로퍼티가 오브젝트에 존재하지 않는다면 `undefined`를 반환한다.
- 첫 번째 인자로는 오브젝트에서 뽑을 프로퍼티명을 지정한다.
- 두 번째 인자로는 대상 오브젝트를 지정한다.
- 결과는 두 번째 인자로 주어진 오브젝트에서 첫 번째 인자로 지정한 명칭의 프로퍼티의 값을 뽑아낸다.
- 만약 오브젝트에서 프로퍼티를 찾을 수 없다면 `undefined`를 반환한다.

## 표현
```
Idx → {s: a} → a | Undefined
Idx = String | Int | Symbol
```
- `Idx → `: 첫 번째 인자로는 인덱스(Idx)를 받는다. 배열의 인덱스가 될 수도 있으며, 오브젝트의 키가 될 수도 있는 값이다.
- `→ {s: a} →`: 두 번째 인자로는 오브젝트를 받는다.
- `→ a | Undefined`: 지정한 Idx에 해당하는 s 프로퍼티를 선택하여 프로퍼티에 대응하는 값 a를 반환한다. 하지만 프로퍼티가 없다면 `undefined`를 반환한다.
- `Idx = String | Int | Symbol`는 Idx가 어떤 것으로 구성되어 있는지에 관한 것이다. 문자열 또는 정수 또는 Symbol 타입이 Idx 타입이다.

## 예제
```js
R.prop('x', {x: 100}); //=> 100
R.prop('x', {}); //=> undefined
R.prop(0, [100]); //=> 100
R.compose(R.inc, R.prop('x'))({ x: 3 }) //=> 4
```
- `R.prop('x', {x: 100});`는 `{x: 100}`에서 'x' 프로퍼티의 값을 뽑으므로 `100`이란 결과가 나온다.
- `R.prop('x', {});`는 `{}`에서 `x` 프로퍼티의 값을 뽑는데 프로퍼티가 존재하지 않으므로 `undefined`를 반환한다.
- `R.prop(0, [100]);` 자바스크립트에서 배열은 인덱스 번호를 프로퍼티로 갖는 오브젝트라고 할 수 있다. 자바스크립트에서 `var['key']` 형식으로 배열이든 오브젝트이든 동일하게 접근할 수 있다. `[100]`은 0번째 인덱스가 `100`이란 값을 가지는 것이다. 따라서 0이란 프로퍼티명에 해당하는 값인 100을 반환한다.
- `R.prop('x')`는 오브젝트를 받아서 오브젝트의 x 프로퍼티의 값을 뽑아내는 함수이며, `R.inc`는 수를 인자로 받아 값을 1 증가시키는 함수이다.
- `R.compose(R.inc, R.prop('x'))`는 할당된 인자를 오른쪽 부터 적용한다. 오브젝트를 받아서 x 프로퍼티를 오브젝트에서 뽑아서 값을 1 증가시키는 함수이다. `({ x: 3 })`이란 인자를 받았기 때문에 x 프로퍼티에 해당하는 3 값을 뽑아서 1을 증가시킨다.

## Reference
- https://ramdajs.com/docs/#prop
