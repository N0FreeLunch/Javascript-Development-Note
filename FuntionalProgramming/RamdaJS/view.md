## view
> Returns a "view" of the given data structure, determined by the given lens.
- 주어진 렌즈에 의해 결정된, 주어진 데이터 구조의 view를 반환한다.
> The lens's focus determines which portion of the data structure is visible.
- 랜즈의 초점은 데이터 구조의 어느 부분을 표시할지를 결정한다.
> See also set, over, lens, lensIndex, lensProp, lensPath.

### 설명
- 렌즈를 사용하여 주어진 데이터 구조에서 원하는 값을 찾는다.

### 표현
```
Lens s a → s → a
```
- `Lens s a`: 첫 번째 인자로 랜즈를 받는다. 자료 구조 s에서 지정한 값을 취득해 a라는 종류의 값을 찾아내는 의미를 가지며, 자바스크립트에서는 일반적으로 오브젝트에서 지정한 프로퍼티의 값을 취득하는 용도로 사용된다. 이 랜즈 표현식에서 지정한 값 곧 프로퍼티에 대한 정보는 없다.
- `→ s →`: 두 번째 인자로 렌즈에 적용할 데이터 스트럭쳐(s) 값을 받는다. 자바스크립트에서는 보통 오브젝트에 해당한다.
- `→ a`: 대상 더미에서 렌즈가 가리키는 부분의 값을 반환한다.

```
Lens s a = Functor f => (a → f a) → s → f s
```
- `Lens s a = Functor f =>`: 펑터 f가 렌즈의 역할을 할 때
- `(a → f a) →`: 첫 번째 인자로 어떤 종류 a의 값에 대해 펑터가 적용된 a를 반환하는 함수를 받고
- `→ s →`: 두 번째 인자로 렌즈에 적용할 대상 자료 구조(s) 값을 받는다.
- `→ f s`: 두 번째 인자로 받은 자료 구조 값에 렌즈 기능의 펑터 f가 적용된 결과 값을 얻는다.

### 예제
```js
const xLens = R.lensProp('x');

R.view(xLens, {x: 1, y: 2});  //=> 1
R.view(xLens, {x: 4, y: 2});  //=> 4
```
- `R.lensProp('x')`로 렌즈를 정의한다. 이 렌즈는 자바스크립트의 오브젝트에 대해 x라는 프로퍼티의 값을 취득하는 역할을 한다. 정의된 렌즈를 `R.view` 함수와 함께 사용하면 오브젝트에서 렌즈에서 지정한 프로퍼티의 값을 취득할 수 있다.
- 오브젝트 `{x: 1, y: 2}`를 받아 x 프로퍼티의 값 1을 반환하고, 오브젝트 `{x: 4, y: 2}`를 받아 x 프로퍼티의 값 4을 반환한다.

## References
- https://ramdajs.com/docs/#view
