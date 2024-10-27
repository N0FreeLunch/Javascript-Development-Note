## applySpec

> Given a spec object recursively mapping properties to functions, creates a function producing an object of the same structure, by mapping each property to the result of calling its associated function with the supplied arguments.
- 속성을 함수에 재귀적으로 매핑하는 사양(spec) 객체가 주어지면, 제공된 인수로 연관된 함수를 호출한 결과에 각 속성을 매핑하여 동일한 구조의 객체를 생성하는 함수를 생성합니다.

> See also [converge](./converge.md), [juxt](./juxt.md).

### 설명

- 특정한 리터럴 오브젝트를 받아서 키에 할당된 값을 미리 설정한 변환 함수에 의해 변경하기 위해 사용한다. 미리 설정한 것을 사양 객체 (spec object)라고 하는데, 사양 객체는 '{키: 함수}' 또는 '{키: {키: 함수}}'의 재귀 형식으로 구성되어 applySpec 함수가 이 객체를 설정값으로 받고 반환된 함수에 특정한 리터럴 오브젝트를 받으면, 각각의 키에 매핑되는 값은 사양 객체의 동일한 키에 할당된 함수에 값을 인자로 넘겨주고 반환된 값을 키의 값으로 하는 리터럴 객체를 반환한다.
- 첫 번째 인자로는 특정 형식의 리터럴 오브젝트를 받는다. 리터럴 오브젝트의 형식은 키-'인자를 받아 평가되는 함수, "키-인자를 받아 평가되는 함수"'의 구조이다. (이 재귀 형식으로 구성된 객체에 적용 가능하다.)
- 두 번째 인자 또는 반환된 함수의 사양 객체의 '인자를 받아 평가되는 함수'에 인자로 할당하고 그 평가된 값을 첫 번째 인자의 리터럴 오브젝트 형식과 일치하게 하면서 '인자를 받아 평가되는 함수' 위치에 평가된 값을 넣은 결과를 반환한다.

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
- `{k: ((a, b, …, m) → v)}`: 첫 번째 인자로 오브젝트를 받으며, 이 오브젝트는 벨류로 특수한 구조의 함수를 받는 구조이다. 오브젝트의 키를 `k`, 오브젝트의 벨류는 `((a, b, …, m) → v)`이다.
- `((a, b, …, m) → v)`: 오브젝트의 키에 대응하는 값은 인자의 수에 제한이 없고 인자의 타입에 제한이 없는 다양한 타입을 받을 수 있다.
- `→ ((a, b, …, m) → {k: v})`: 반환된 함수는 `(a, b, …, m)` 값을 넣어 주면 `→ {k: v}`라는 오브젝트 형식의 값이 나오고 `v`는 첫 번째 인자의 `((a, b, …, m) → v)` 부분에 따라 `(a, b, …, m)` 타입에 해당하는 값을 받았을 때 평가되는 결과 값 `v`를 반환되는 리터럴 오브젝트의 벨류 값으로 함

- 타입은 첫 번째 인자의 오브젝트의 벨류가 되는 함수의 인자와 동일한 타입의 인자를 넣어 줘야 하기 때문에 `(a, b, …, m)`가 된다.

### 예제
```js
const getMetrics = R.applySpec({
  sum: R.add,
  nested: { mul: R.multiply }
});
getMetrics(2, 4); // => { sum: 6, nested: { mul: 8 } }
```
- `R.applySpec` 함수는 인자로 리터럴 오브젝트를 받았다.
```
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
