## constructN

## 설명
> Wraps a constructor function inside a curried function that can be called with the same arguments and returns the same type. The arity of the function returned is specified to allow using variadic constructor functions.
- 생성자 함수를 레핑한 함수이다. 이 함수는 커링되어 있으며 동일한 인자와 인자와 동일한 리턴타입으로 호출되는 함수이다. 이 함수의 인자의 수(arity)는 지정되어 있으며 가변 생성자 함수에 사용할 수 있다.

## 설명
- 자바스크립트의 생성자로 사용될 수 있는 함수를 레핑하여 지정한 수의 인자를 할당하면 해당 인자가 생성자의 인자로 할당된 새로운 객체를 생성하는 함수를 만든다.
- 받을 수 있는 인자의 갯수가 정해져 있기 때문에 커링될 수 있다.

## 표현
```
Number → (* → {*}) → (* → {*})
```
- `Number → ` 첫 번째 인자로 생성자 함수가 몇 개의 인자를 받을 것인지를 정한다.
- `→ (* → {*}) →` 두 번째 인자로 생성자 함수를 받는다. 이 생성자 함수는 생성자 인자를 받아 객체(`{*}`)를 생성하는 함수이다.
- `→ (* → {*})` 평가되어 반환된 함수는 생성자 함수의 인자와 반환 타입을 그대로 갖는 함수이다.

## 예제
```
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
```
function Salad() {
  this.ingredients = arguments;
}
```
- `arguments`는 자바스크립트 키워드로써 사용된 컨텍스트의 함수가 갖는 인자 리스트를 배열로 가지고 있는 함수이다.
- 이 함수의 파라메터는 지정되어 있지 않지만, 인자를 할당하면 할당된 인자만큼을 `arguments`가 가지고 있는 형태가 된다.

#### 생성자 함수의 오브젝트에 멤버 메소드 추가하기
```
Salad.prototype.recipe = function() {
  const instructions = R.map(ingredient => 'Add a dollop of ' + ingredient, this.ingredients);
  return R.join('\n', instructions);
};
```

#### 생성자 함수를 constructN 함수로 레핑하기
```
const ThreeLayerSalad = R.constructN(3, Salad);
```
- `Salad`라는 함수는 생성자로 사용되었고 이 생성자 함수를 `R.constructN` 함수에 넣었다.
- 인자를 3개 받아서 생성자 함수가 실행되도록 하였다.

#### 레핑한 생성자 함수 호출하기
```
const salad = ThreeLayerSalad('Mayonnaise')('Potato Chips')('Ketchup');
```
- 레핑된 생성자 함수를 호출하면 앞서 만든 생성자 함수와 멤버 메소드를 갖는 새로운 오브젝트가 생성된다.

#### 생성된 객체의 멤버 
```
salad.recipe()
```
- `constructN`으로 레핑한 생성자 함수에 할당한 인자에 따른 결과값을 갖는 것을 확인할 수 있다.
- `R.map(ingredient => 'Add a dollop of ' + ingredient, ['Mayonnaise', 'Potato Chips', 'Ketchup'])`에 해당하는 결 갖는다.

## Reference
- https://ramdajs.com/docs/#constructN
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments
