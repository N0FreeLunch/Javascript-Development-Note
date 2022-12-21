## map
> Takes a function and a functor, applies the function to each of the functor's values, and returns a functor of the same shape.
- 하나의 함수와 하나의 펑터을 인자로 받아 각각의 해당 펑터의 값에 함수를 적용한다. 그리고 동일한 형태의 펑터를 반환한다

> Ramda provides suitable map implementations for Array and Object, so this function may be applied to [1, 2, 3] or {x: 1, y: 2, z: 3}.
- Ramda는 배열과 오브젝트의 적절한 맵 구현체들을 제공하기 때문에 배열 `[1, 2, 3]`나 오브젝트 `{x: 1, y: 2, z: 3}` 등에 적용될 수 있다.

> Dispatches to the map method of the second argument, if present.

> Acts as a transducer if a transformer is given in list position.

> Also treats functions as functors and will compose them together.

## 설명
- 기본적으로 함수형 언어에서 map이란 구현체는 펑터에 적용이 된다. 자바스크립트에서는 리스트나 오브젝트라는 구현체에 펑터를 적용 시키면 펑터가 적용된 결과 값을 갖는다.
- 펑터란 값의 연산을 위해 미리 만들어 놓은 식과 같은 의미를 가진다. 리스트나 오브젝트라는 구현체가 없는 펑터라는 식에도 펑터에 map이란 식을 추가할 수 있다는 것이 본질이다.
- 펑터에 map을 적용하면 새로운 펑터가 만들어진다. 기존 펑터에 정의한 map 연산이 추가된 결과를 만드는 펑터가 된다.
- 첫 번째 인자로는 함수를 받고, 두 번째 인자로는 펑터를 받는다. 이 펑터는 구현체가 없는 연산식의 의미에 해당하는 펑터일 수도 있고, 배열이나 오브젝트로 값이 이미 존재하는 펑터일 수도 있다.
- 두 번째 인자로 받은 펑터의 각각의 값에 첫 번째 인자로 받은 함수를 적용한 펑터를 반환하며, 두 번째 인자로 받은 펑터의 각각의 값이 배열 또는 오브젝트 등으로 구현되어 있는 상태라면 구현된 형태의 결과값인 주어진 구현체가 배열이면 배열으로 오브젝트면 오브젝트로 반환한다.

## 표현
```
Functor f => (a → b) → f a → f b
```
- `Functor f =>` f를 펑터라고 하자.
- `(a → b) →` 첫 번째 인자로 함수를 받는다.
- `→ f a` 두 번째 인자로 어떤 타입(a)으로 구성된 펑터를 받는다.
- `→ f b` 두 번째 인자로 받은 펑터가 가진 각각의 값에 첫 번째 인자로 받은 함수를 적용한 펑터를 반환한다.

## 예제
```
const double = x => x * 2;

R.map(double, [1, 2, 3]); //=> [2, 4, 6]

R.map(double, {x: 1, y: 2, z: 3}); //=> {x: 2, y: 4, z: 6}
```
- map의 첫 번째 인자로 `x => x * 2` 라는 함수를 받았다.
- `[1, 2, 3]` map의 두 번째 인자로 배열이라는 구현체를 받았다. ramda는 식으로서의 펑터 뿐만 아니라 펑터에 값이 적용된 형태의 펑터인 배열에 대해 펑터 각각의 값인 배열의 각 원소에 주어진 함수를 적용하여 같은 형식의 결과 값을 반환하므로 `[2, 4, 6]`가 된다.
- `{x: 1, y: 2, z: 3}` map의 두 번째 인자로 오브젝트라는 구현체를 받았다. ramda는 식으로서의 펑터 뿐만 아니라 펑터에 값이 적용된 형태인 오브젝트에 대해 펑터 각각의 값인 오브젝트의 각 원소에 주어진 함수를 적용하여 같은 형식의 결과 값을 반환하므로 `{x: 2, y: 4, z: 6}`가 된다.

## Reference
- https://ramdajs.com/docs/#map
