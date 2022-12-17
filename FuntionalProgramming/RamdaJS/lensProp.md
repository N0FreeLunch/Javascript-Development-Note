## lensProp
> Returns a lens whose focus is the specified property.
- 특정하게 지정된 프로퍼티에 초점을 맞추는 랜즈를 반환한다.

## 설명
- 하나의 인자를 받으며 문자열을 받아 해당 문자열에 매칭되는 프로퍼티를 주어지는 키가 갖는 값을 선택하는 랜즈를 반환한다.

## 표현
```
String → Lens s a
Lens s a = Functor f => (a → f a) → s → f s
```
- `String →` 첫 번째 인자로 문자열을 받는다.
- `→ Lens s a` 인자 하나를 받아 랜즈를 반환한다.

## 예제
```
const xLens = R.lensProp('x');

R.view(xLens, {x: 1, y: 2});            //=> 1
R.set(xLens, 4, {x: 1, y: 2});          //=> {x: 4, y: 2}
R.over(xLens, R.negate, {x: 1, y: 2});  //=> {x: -1, y: 2}
```
- `R.lensProp('x')`는 `'x'`라는 프로퍼티의 값을 오브젝트에서 선택하라는 랜즈를 반환한다.
- `R.view(xLens, {x: 1, y: 2})` 주어진 오브젝트에서 랜즈에 의해 프로퍼티 `x`의 값인 `1`이 반환된다.
- `R.set(xLens, 4, {x: 1, y: 2})` 주어진 오브젝트에서 랜즈에 의해 프로퍼티 `x`의 값인 `1`이 `4`로 바뀐 새 오브젝트를 반환한다.
- `R.over(xLens, R.negate, {x: 1, y: 2})` 주어진 오브젝트에서 랜즈에 의해 프로퍼티 `x`의 값인 `1`이 `R.negate` 함수에 의해 변환된 `-1`로 변환된 새 오브젝트를 반환한다.


## Reference
- https://ramdajs.com/docs/#lensProp
