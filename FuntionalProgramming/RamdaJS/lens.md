## lens
> Returns a lens for the given getter and setter functions. 
- getter과 setter 함수가 주어졌을 때 'lens'라는 함수를 반환한다.

> The getter "gets" the value of the focus; the setter "sets" the value of the focus. 
- getter은 지정된 값을 가져오는 역할을 하며 setter는 지정된 값을 정의하는데 사용한다.

> The setter should not mutate the data structure.
- settter은 대상이 되는 데이터 구조의 데이터의 상태를 변경하지 않아야 한다.

## 설명
- 함수형 언어에서 사용하는 Lens란 특성을 가진 대상을 반환한다. 순수 함수형 언어에서 Lens는 하나의 타입으로 정해진 만큼 Lens는 특수한 성격을 갖는다.
- Lens 특성은 자료구조 내의 값을 조회, 변경 또는 자료구조에 값을 생성하기 위해 사용한다.

## 표현
```
(s → a) → ((a, s) → s) → Lens s a
Lens s a = Functor f => (a → f a) → s → f s
```
- `(s → a)` 첫 번째 인자로 getter 함수를 받는다. getter 함수는 대상 데이터 구조에서 주어진 문자열(s)에 매칭되는 키가 가진 값을 뽑아낼 수 있는 함수이다. 
- `→ ((a, s) → s) →` 두 번째 인자로 setter 함수를 받는다. setter 함수는 첫번째 인자로 다양한 타입의 값(a)과 두 번째 인자로 문자열(s)을 받아서 두 번째 인자를 키로 하고 첫 번째 인자를 벨류로 하는 키-벨류 세트를 대상 데이터 구조에 집어 넣는 기능을 가진다.
- `Lens s a`라는 표현을 살펴보자. `Lens s a = Functor f`라고 표현하고 있다. Functor는 어떠한 자료구조를 자료구조의 직접적인 변경 없이 Functor 함수를 사용하는 것만으로 해당 자료구조의 데이터를 조작하여 변경된 결과를 주어진 자료구조의 직접적인 변경 없이 복사 또는 생성을 통해서 값을 얻을 수 있는 기능을 의미한다.
- `Functor f =>` Functor 함수는 다음과 같이 정의한다. `(a → f a) → s → f s`
- `(a → f a)` 
- `→ s` 
- `→ f s`
- `→ Lens s a`

## 예제
```
const xLens = R.lens(R.prop('x'), R.assoc('x'));

R.view(xLens, {x: 1, y: 2});            //=> 1
R.set(xLens, 4, {x: 1, y: 2});          //=> {x: 4, y: 2}
R.over(xLens, R.negate, {x: 1, y: 2});  //=> {x: -1, y: 2}
```
- `xLens`는 펑터에 해당하는 lens이다. `R.lens`함수로 만들어 졌으며 `R.prop('x')` 객체를 받아서 `x` 프로퍼티의 값을 반환하는 함수를 첫 번째 인자로 받았고, `R.assoc('x')` 객체를 받아서 해당 객체의 x 프로터티의 값을 존재하지 않는 다면 정의하고 프로퍼티가 존재한다면 `x`값을 변경하는 함수를 받았다.
- `R.prop('x')`는 오브젝트 하나를 받아서 평가가 되는 반면, `R.assoc('x')`는 x프로퍼티에 할당할 값과 대상 오브젝트를 각각 하나의 인자에 할당한 후 평가한다.
- `R.view`는 랜즈 펑터인 xLens에 오브젝트 하나를 인자로 주어 해당 오브젝트의 x 프로퍼티의 값을 뽑아내는 기능을 한다.
- `R.set`는 렌즈 펑터인 xLens에 프로퍼티 변경할 프로퍼티 값을 지정하고 대상 오브젝트를 주어 주어진 오브젝트의 x 프로퍼티 값을 바꾼 새 오브젝트를 반환한다.
- `R.over`는 렌즈 펑터인 xLens에 프로퍼티의 값을 넣어 다른 값으로 변경하는 함수와 오브젝트를 받아 주어진 오브젝트에서 x프로퍼티 값을 주어진 함수에 넣어 반환된 값으로 바꾼 새 오브젝트를 반환한다.

## Refernece
- https://ramdajs.com/docs/#lens
