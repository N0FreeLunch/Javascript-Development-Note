## applySpec

> Given a spec object recursively mapping properties to functions, creates a function producing an object of the same structure, by mapping each property to the result of calling its associated function with the supplied arguments.
- 속성을 함수에 재귀적으로 매핑하는 사양(spec) 객체가 주어지면, (사양 객체의) 각각의 프로퍼티에 연관된 함수를 호출한 결과를 매핑한 (사양 객체와) 동일한 구조의 오브젝트를 만들어내는 함수를 생성한다.

> See also [converge](./converge.md), [juxt](./juxt.md).

### 설명

- 동일한 인자를 받는 여러 함수에 인자를 전달할 때, 한 번만 인자를 전달하여, 여러 함수에 전달한 평가 결과를 얻는 용도로 사용한다. 여러 함수가 키의 값으로 매핑된 사양 객체(spec object)를 받아 반환된 함수에 인자를 전달하면 사양 객체의 매핑된 함수에 이 값을 전달하고, 사양 객체와 동일한 구조의 오브젝트의 키에 함수의 결과값이 매핑된 오브젝트를 얻는다.
- 첫 번째 인자로는 특정 형식의 리터럴 오브젝트를 받는다. 리터럴 오브젝트의 형식은 키-"인자를 받아 평가되는 함수, '키-인자를 받아 평가되는 함수'"의 구조이다. 사양 객체는 '{키: 함수}' 또는 '{키: {키: 함수}}'의 형태로 재귀 형태로 오브젝트를 구성할 수 있다.
- 사양 객체를 applySpec 함수의 인자로 넣어 평가되어 반환된 함수에 인자를 전달하면, 사양 객체에 매핑된 함수에 동일한 인자를 전달하고, 사양 객체의 함수 값 위치에 해당 함수의 평가된 값이 매핑된 오브젝트를 얻는다.

### 문법

```
R.applySpec(spec): function
```
- `spec`: an object recursively mapping properties to functions for producing the values for these properties.
- Returns function A function that returns an object of the same structure as `spec', with each property set to the value returned by calling its associated function with the supplied arguments.

### 표현

```
{k: ((a, b, …, m) → v)} → ((a, b, …, m) → {k: v})
```
- `{k: ((a, b, …, m) → v)}`: 첫 번째 인자로 오브젝트를 받으며, 이 오브젝트는 벨류로 동일한 구성의 인자를 받는 함수를 가진 구조로 사양 객체라고 불린다. 오브젝트의 키를 `k`로 나타내고, 오브젝트의 벨류는 동일한 인자 구성의 함수 `((a, b, …, m) → v)`으로 나타낸다. 오브젝트의 키에 대응하는 값은 인자의 수에 제한이 없고 인자의 타입에 제한이 없는 다양한 타입을 받을 수 있지만, 매핑된 모든 함수는 동일한 인자 타입과 인자 갯수를 받아야 한다.
- `→ ((a, b, …, m) → {k: v})`: 반환된 함수에 인자들`(a, b, …, m)`을 전달하면, 사양 객체에 매핑된 함수에 인자를 전달하고, 각각의 함수가 인자가 전달되어 평가된 값을 가진 객체의 구조 `→ {k: v}`를 갖는다. `v`는 첫 번째 인자의 `((a, b, …, m) → v)` 부분에 따라 `(a, b, …, m)`에 해당하는 값을 받았을 때 평가되는 결과 값 `v`가 된다.

### 예제
```js
const getMetrics = R.applySpec({
  sum: R.add,
  nested: { mul: R.multiply }
});
getMetrics(2, 4); // => { sum: 6, nested: { mul: 8 } }
```
- `R.applySpec` 함수는 인자로 리터럴 오브젝트를 받았다.
```js
{
  sum: R.add,
  nested: { mul: R.multiply }
}
```
- 첫 번째 인자의 리터럴 오브젝트는 '키-벨류' 형식에서 벨류값이 인자를 받아 평가를 기다리는 함수 또는 이런 함수가 들어가 있는 리터럴 오브젝트로 되어 있다.
- 두 번째 인자부터 받은 인자는 순차적으로 리터럴 오브젝트 내부의 '인자를 받아 평가를 기다리는 함수'의 인자로 들어가서 리터럴 오브젝트 내부의 함수는 평가된다.
- 첫 번째 인자에 지정한 리터럴 오브젝트의 구조에 따라서 결과 값을 반환한다. 이 때, 리터럴 오브젝트 내의 '인자를 받아 평가를 기다리는 함수'가 함수가 평가되어 결과 값으로 바뀐 형태의 동일 형태의 리터럴 오브젝트를 반환 받는다.

### References
- https://ramdajs.com/docs/#applySpec
- https://github.com/ramda/ramda/blob/master/test/applySpec.js
- https://github.com/ramda/types/blob/develop/types/applySpec.d.ts
