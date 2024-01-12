## of
> Given a constructor and a value, returns a new instance of that constructor containing the value.
- 생성자와 값을 하나씩 받아서 새로운 인스턴스를 반환한다. 이 인스턴스는 받은 값을 포함한다.

> Dispatches to the fantasy-land/of method of the constructor first (if present) or to the of method last (if present). When neither are present, wraps the value in an array.

> Note this of is different from the ES6 of; See https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/of

### 설명
- 자바스크립트는 함수에 `new` 키워드를 사용하면, 새로운 인스턴스 하나를 만든다. 이때, 함수는 생성자의 역할을 하는 함수여야 인스턴스가 생성된다.
- 생성자와 값을 하나 받아서 생성자로 부터 새로운 인스턴스를 반환하는 함수이다.
- 전달 받은 생성자를 `constructor`라고 하고 전달 받은 값을 `value`라고 하면 `of` 함수가 반환하는 결과는 `(new 생성자(value))`가 된다.

### 표현
```
(* → {*}) → a → {a}
```
- `(* → {*}) →`는 생성자를 의미한다. 어떤 값을 받아서 인스턴스(객체)를 반환하는 함수를 받는다.
- `→ a → ` 값을 하나 받는다.
- `→ {a}` 두 번째 인자 값이 세팅된 인스턴스를 반환한다.

### 예제
```js
R.of(Array, 42);   //=> [42]
R.of(Array, [42]); //=> [[42]]
R.of(Maybe, 42);   //=> Maybe.Just(42)
```
- `R.of(Array, 42)`는 `new Array(42)`를 반환한다. 따라서 그 결과값은 `[42]`이다.
- `R.of(Array, [42])`는 `new Array([42])`를 반환한다. 따라서 그 결과값은 `[[42]]`이다.
- `R.of(Maybe, 42)`는 `new Maybe(42)`를 반환한다. 따라서 그 결과 값은 `Maybe.Just(42)`이다.

## Reference
- https://ramdajs.com/docs/#of
