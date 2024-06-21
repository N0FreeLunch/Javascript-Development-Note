## set
> Returns the result of "setting" the portion of the given data structure focused by the given lens to the given value.

> See also view, over, lens, lensIndex, lensProp, lensPath.

### 설명
- view, over, set과 같은 함수에 대상에서 특정한 프로퍼티를 뽑아내기 위한 설정을 담은 lens 함수와 함께 사용되어, set 함수는 랜즈 함수에서 지정한 프로퍼티의 값을 생성하거나 변경하는 용도로 사용한다.

### 표현
```
Lens s a → a → s → s
Lens s a = Functor f => (a → f a) → s → f s
```

#### 펑터로 사용되지 않은 렌즈
- `Lens s a →`: 첫 번째 인자는 렌즈를 받는다. 렌즈는 대상의 타입 파라메터를 s라고 했을 때 s의 프로퍼티 a를 뽑는 렌즈이다.
- `→ s →`: 두 번째 인자로는 렌즈를 적용할 대상을 받는다. 대상의 타입 파라메터는 s인데 첫 번째 인자로 받은 렌즈에서 프로퍼티를 뽑을 수 있는 대상인 s와 동일한 타입이 되어야 한다.
- `→ s`: 최종 결과는 렌즈가 받는 타입 파라메터 s를 반환한다. 이 타입 파라메터 s는 렌즈로 a 타입의 프로퍼티를 뽑아낼 수 있는 대상이다.

#### 펑터로 사용된 렌즈
- `Lens s a = Functor f =>`: 주어진 렌즈가 펑터의 역할을 할 때 (펑터란 한 모나드에서 다른 모나드의 구조에서 사용될 수 있도록 전환하는 것을 의미한다.)
- `(a → f a) →`: 첫 번째 인자로는 인자 a를 받아, 펑터가 적용된 a를 반환하는 함수를 받는다. `Lens s a `와 달리 `f a`는 렌즈에 `a`가 적용된 렌즈로, s만 받으면 되는 함수 `f a`를 반환한다. `Lens s a → a → s → s` 구조에서는 프로퍼티를 받았지만, 프로퍼티 a가 적용된 렌즈를 반환하는 함수를 받는다.
- `→ s →`: 두 번째 인자로는 프로퍼티를 추출할 수 있는 대상 예를 들어 오브젝트를 반환한다.
- `→ f s`: 펑터가 적용된 결과값을 반환한다.

### 예제
```js
const xLens = R.lensProp('x');

R.set(xLens, 4, {x: 1, y: 2});  //=> {x: 4, y: 2}
R.set(xLens, 8, {x: 1, y: 2});  //=> {x: 8, y: 2}
```
- 오브젝트에서 지정한 프로퍼티의 값을 꺼내기 위한 lens 함수를 만드는 `R.lensProp` 함수를 사용하여 프로퍼티 `'x'`를 추출하는 `xLens` 함수를 받는다.
- `R.set`은 x 프로퍼티를 뽑는 xLens 함수를 받고, 해당 프로퍼티의 값이 없다면 생성하고 있다면 변경하는 값을 받는다. 4를 받으면 x 프로퍼티의 값은 4로 변경이 되고, 8을 받으면 x 프로퍼티의 값은 8로 변경이 된다.
- `R.set(xLens, 4, {x: 1, y: 2})`에서 x 프로퍼티로 4를 지정했으므로 결과는 `{x: 8, y: 2}`이 되고, `R.set(xLens, 8, {x: 1, y: 2})`에서 x프로퍼티로 8을 지정했으므로 결과는 `{x: 8, y: 2}`가 된다.

## Referece
- https://ramdajs.com/docs/#set
