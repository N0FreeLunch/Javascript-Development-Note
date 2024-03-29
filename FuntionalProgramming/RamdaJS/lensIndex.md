## lensIndex
> Returns a lens whose focus is the specified index.
- 특정한 인덱스를 지정하한 lens를 반환한다.

## 설명
- 배열에서 인덱스를 기반으로 값을 원소를 선택하는 랜즈를 반환한다.
- 인자를 하나만 받으며 첫 번째 인자로 인덱스 번호를 받으면 랜즈를 반환한다.
- 해당 랜즈에 `R.view`, `R.set`, `R.over` 등으로 인자를 전달하고 대상 배열을 지정하면 주어진 배열에서 지정한 인덱스에 해당하는 값을 선택하게 된다.

## 표현
```
Number → Lens s a
Lens s a = Functor f => (a → f a) → s → f s
```
- `Number →` 첫 번째 인자로 인덱스 번호에 해당하는 수를 받는다.
- `→ Lens s a` 랜즈를 반환한다.
- `Lens s a = Functor f => (a → f a) → s → f s`는 랜즈 `Lens s a`의 정의는 펑터 `f`라고 할 때 렌즈의 정의는 `(a → f a) → s → f s`라는 의미이다.
- 펑터의 인자는 함수의 인자와 다르며 펑터에 인자를 전달하기 위해서는 `R.view`, `R.set`, `R.over`등의 함수에 랜즈와 랜즈의 펑터 인자에 전달할 인자를 할당해야 한다.
- `(a → f a) →` 첫 번째 인자로 자료 구조 내의 특정 데이터 값을 다른 값으로 변환하는 함수를 받는다.
- `→ s →` 두 번째 인자로 자료 구조 내에서 대상이 되는 데이터를 지정하는 값을 받는다.
- `→ f s` 두 번째 인자로 받은 값으로 자료 구조 내에서 데이터를 선택하고 선택된 데이터를 첫 번째 인자의 함수를 통해서 바꾼 새로운 데이터 셋을 반환한다.

## 예제
```
const headLens = R.lensIndex(0);

R.view(headLens, ['a', 'b', 'c']);            //=> 'a'
R.set(headLens, 'x', ['a', 'b', 'c']);        //=> ['x', 'b', 'c']
R.over(headLens, R.toUpper, ['a', 'b', 'c']); //=> ['A', 'b', 'c']
```
- `R.lensIndex(0)` 첫배열에서 인덱스 번호가 0번인 첫번째 인덱스를 선택하는 렌즈를 반환한다.
- `R.view(headLens, ['a', 'b', 'c'])` 주어진 배열에서 첫 번째 인덱스를 선택하라는 렌즈에 맞게 인덱스를 선택한 후 해당 인덱스의 값인 `'a'`를 반환한다.
- `R.set(headLens, 'x', ['a', 'b', 'c'])` 주어진 배열에서 첫 번째 인덱스를 선택하하는 렌즈에 맞게 해당 인덱스를 선택한 후 값을 `'x'`로 바꾼 새 배열을 반환한다.
- `R.over(headLens, R.toUpper, ['a', 'b', 'c'])` 주어진 배열에서 첫 번째 인덱스를 선택하하는 렌즈에 맞게 인덱스를 선택한 후 해당 인덱스의 값을 `R.toUpper`로 전달했을 때 반환되는 결과 값으로 바꾼 새 배열을 반환한다.

## Reference
- https://ramdajs.com/docs/#lensIndex
