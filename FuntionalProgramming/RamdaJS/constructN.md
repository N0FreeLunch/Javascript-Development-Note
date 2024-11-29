## constructN

> Wraps a constructor function inside a curried function that can be called with the same arguments and returns the same type. The arity of the function returned is specified to allow using variadic constructor functions.
- 생성자 함수를 레핑한 함수이다. 이 함수는 커링되어 있으며 레핑된 함수와 동일한 인자와 인자와 동일한 리턴타입으로 호출되는 함수이다. 이 함수의 인자의 수(arity)는 지정되어 있으며 가변 생성자 함수에 사용할 수 있다.

### 설명

- 인자를 무한정 받는 함수를 평가하기 위해 일정한 갯수의 인자가 주어지면 평가가 일어날 수 있는 `construct` 함수가 바로 `constructN`에 해당한다.
- 자바스크립트의 생성자로 사용될 수 있는 함수를 레핑하여 레핑한 함수에 지정한 수의 인자를 할당하면 레핑한 함수에 전달된 인자가 레핑된 생성자의 인자로 할당되어 새로운 객체를 생성하게 만든다. `construct` 함수와 마찬가지로 커링된 함수를 반환한다.
- `construct` 함수가 인자의 수가 정해진 생성자 함수에 사용할 수 있었던 반면, 인자의 수가 가변인 경우 `construct`으로 감싼 함수를 사용했을 때 함수가 반환되지 않는 문제가 생긴다. 자바스크립트에서 함수는 함수가 받는 인자의 갯수를 확인하는 [Function.prototype.length](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/length)이란 함수가 있다. `construct`는 함수의 인자의 수를 확인해서 내부적으로는 `constructN`을 실행한다. `constructN(0, fn)`이 되므로 바로 fn의 평가된 결과를 얻어 인자를 받을 수 없게 된다.

### 문법

```
R.constructN(N, Fn): function
```

> `n`: The arity of the constructor function.
- `n`: 생성자 함수의 인자의 갯수
> `Fn`: The constructor function to wrap.
- `Fn`: 레핑할 생성자 함수
> Returns function A wrapped, curried constructor function.
- 함수를 반환한다. 이 함수는 생성자 함수를 감싸고 커링한다.

### 표현

```
Number → (* → {*}) → (* → {*})
```

- `Number → `: 첫 번째 인자로 생성자 함수가 몇 개의 인자를 받을 것인지를 정한다.
- `→ (* → {*}) →`: 두 번째 인자로 생성자 함수를 받는다. 이 생성자 함수는 생성자 인자를 받아 객체(`{*}`)를 생성하는 함수이다.
- `→ (* → {*})`: 평가되어 반환된 함수는 생성자 함수의 인자와 반환 타입을 그대로 갖는 함수이다.

### 예제

```js
// Variadic Constructor function
function Salad() {
  this.ingredients = arguments;
}

Salad.prototype.recipe = function() {
  const instructions = R.map(ingredient => 'Add a dollop of ' + ingredient, this.ingredients);
  return R.join('\n', instructions);
};

const ThreeLayerSalad = R.constructN(3, Salad);

// Notice we no longer need the 'new' keyword, and the constructor is curried for 3 arguments.
const salad = ThreeLayerSalad('Mayonnaise')('Potato Chips')('Ketchup');

console.log(salad.recipe());
// Add a dollop of Mayonnaise
// Add a dollop of Potato Chips
// Add a dollop of Ketchup
```

#### 생성자 함수 만들기

```js
function Salad() {
  this.ingredients = arguments;
}
```
- `arguments`는 자바스크립트 키워드로써 사용된 컨텍스트의 함수가 갖는 인자 리스트를 배열로 가지고 있는 함수이다.
- 이 함수의 파라메터는 지정되어 있지 않지만, 인자를 할당하면 할당된 인자만큼을 `arguments`가 가지고 있는 형태가 된다.

#### 생성자 함수의 오브젝트에 멤버 메소드 추가하기

```js
Salad.prototype.recipe = function() {
  const instructions = R.map(ingredient => 'Add a dollop of ' + ingredient, this.ingredients);
  return R.join('\n', instructions);
};
```

#### 생성자 함수를 constructN 함수로 레핑하기

```js
const ThreeLayerSalad = R.constructN(3, Salad);
```
- `Salad`라는 함수는 생성자로 사용되었고 이 생성자 함수를 `R.constructN` 함수에 넣었다.
- 인자를 3개 받아서 생성자 함수가 실행되도록 하였다.

#### 레핑한 생성자 함수 호출하기

```js
const salad = ThreeLayerSalad('Mayonnaise')('Potato Chips')('Ketchup');
```
- 레핑된 생성자 함수를 호출하면 앞서 만든 생성자 함수와 멤버 메소드를 갖는 새로운 오브젝트가 생성된다.

#### 생성된 객체의 멤버

```js
salad.recipe()
```
- `constructN`으로 레핑한 생성자 함수에 할당한 인자에 따른 결과값을 갖는 것을 확인할 수 있다.
- `R.map(ingredient => 'Add a dollop of ' + ingredient, ['Mayonnaise', 'Potato Chips', 'Ketchup'])`에 해당하는 결 갖는다.

## References
- https://ramdajs.com/docs/#constructN
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments
- https://github.com/ramda/ramda/blob/master/test/constructN.js
- https://github.com/ramda/types/blob/develop/types/constructN.d.ts
