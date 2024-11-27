## construct

> Wraps a constructor function inside a curried function that can be called with the same arguments and returns the same type.
- 생성자 함수를 커링된 함수로 감싼다. 레핑된 함수는 생성자 함수와 동일한 인자와 리턴 타입을 가진 함수로써 호출된다.
> See also [invoker](./invoker.md).

### 설명

- 자바스크립트에서 `function` 키워드로 만든 함수는 오브젝트에 해당한다. 이 함수 내부({} 안에)에 오브젝트의 내부의 멤버를 `this.멤버`형식으로 키워드롤 만들 수 있는데 이를 통해서 오브젝트의 멤버의 초기 값을 설정할 수 있다. 이를 `new 함수명`을 통해서 객체를 찍어내는 것이 아니라 `construct` 함수로 객체를 생성하는 함수를 감싸서 객체를 찍어낼 수 있도록 한다.
- `new 함수명(인자들...)`에서 인자를 한꺼번에 다 받아야 하는 반면에 `construct` 함수로 레핑된 함수는 커링되어 있기 때문에 인자를 분리해서 받을 수 있다.
- 자바스크립트에서 `this`는 함수가 호출될 때, 런타임 상태에서 함수가 바인딩 된 위치를 가리킨다. 예를 들어 `function Animal(kind) { this.kind = kind; };` 함수를 그냥 `Animal('value')`으로 호출하면 `this`는 window 객체를 가리킨다. 하지만, `new` 키워드를 사용해서 `new Animal('value')`으로 호출하면, `kind` 멤버는 오브젝트에 바인딩 된 형태가 되어 `{ kind: 'value'}`가 되며, `this`는 오브젝트 `{ kind: 'value'}`를 가리킨다. 만약 `new` 키워드를 사용하고 싶지 않다면 `function Animal(kind) { const binder = {}; binder.kind = kind; console.log(binder); return binder };`와 같이 반환 값에 `this`로 바인딩한 값을 전달해야 한다.
- 감싸이는 함수는 `new` 키워드를 써서 바인딩 될 대상이 오브젝트가 되든지, `new` 키워드를 사용하지 않을 경우 함수의 호출 결과가 객체를 반환하는 형태가 되어야 한다.

### 문법

```
R.construct(fn): function
```
> `fn`: The constructor function to wrap.
- `fn`: 레핑할 생성자 함수
> Returns function. A wrapped, curried constructor function.
- 함수를 반환한다. 이 함수는 생성자 함수가 레핑되고 커링된 것이다.

### 표현

```
(* → {*}) → (* → {*})
```
- `(* → {*}) →`: 첫 번째 인자로 함수를 받는다. 이 함수는 임의의 인자(`*`)를 받고, `new` 키워드로 `this`가 바인딩 될 객체를 새로 생성하든지, 함수의 반환 값이 객체를 반환하는 형태여야 한다. 단순히 시그니처상으로는 인자로 전달된 종류(`*`)와 반환된 종류 (`{*}`)는 서로 다를 수 있지만, 생성자의 의미를 나타내도록 전달된 인자가 반환 객체에 바인딩된 형태를 가지는 것이라 볼 수도 있다.
- `→ (* → {*})`: 반환된 함수는 동일하게 인자를 받아서 동일한 결과를 반환하는 함수이다. 표현식으로는 동일하지만 첫 번째 인자로 받은 함수가 `new`를 통해서 새로운 객체를 생성해야하는 경우에도 반환된 함수를 호출하여 새로운 객체를 생성할 수 있다. 또한 함수가 커링되어 있으므로 인자를 나누어 받을 수 있다.

### 예제

```js
// Constructor function
function Animal(kind) {
  this.kind = kind;
};
Animal.prototype.sighting = function() {
  return "It's a " + this.kind + "!";
}

const AnimalConstructor = R.construct(Animal)

// Notice we no longer need the 'new' keyword:
AnimalConstructor('Pig'); //=> {"kind": "Pig", "sighting": function (){...}};

const animalTypes = ["Lion", "Tiger", "Bear"];
const animalSighting = R.invoker(0, 'sighting');
const sightNewAnimal = R.compose(animalSighting, AnimalConstructor);
R.map(sightNewAnimal, animalTypes); //=> ["It's a Lion!", "It's a Tiger!", "It's a Bear!"]
```

#### Animal 객체의 생성자 만들기
```js
function Animal(kind) {
  this.kind = kind;
};
```

#### Animal 객체의 메소드 추가하기

```js
Animal.prototype.sighting = function() {
  return "It's a " + this.kind + "!";
}
```

#### Animal 객체에 R.construct 함수 사용하기

```js
const AnimalConstructor = R.construct(Animal)
```
```js
AnimalConstructor('Pig')
```
- `construct` 함수에 객체 `Animal`을 인자로 넣어 반환된 함수(`AnimalConstructor`)에 인자를 넣으면 받은 인자와 동일한 인자가 생성자에 할당된 객체를 반환한다 따라서 `{"kind": "Pig", "sighting": function (){...}};` 생성자로 `"kind"`에 `"Pig"`가 할당된 값의 객체가 반환된다.

#### invoker 함수 설정하기

- `const animalSighting = R.invoker(0, 'sighting')`는 지정한 객체에서 `sighting`라는 메소드를 인자없이 호출하는 함수를 반환한다. `animalSighting` 함수는 인자 없이 호출되는 함수이다.

#### 객체 생성을 생략하고 객체의 메소드만을 실행하는 함수 만들기

- `const sightNewAnimal = R.compose(animalSighting, AnimalConstructor);`는 `AnimalConstructor`에 의해서 인자로 생성자에 할당할 인자를 전달하고 해당 생성자로 만들어진 객체를 반환한다. 이 객체에 대해 `animalSighting`로 `sighting`함수를 실행하겠다는 의미를 가진 함수가 `sightNewAnimal` 함수이다.

#### 주어진 리스트로 부터 만들어진 객체의 메소드만 실행한 결과를 리스트로 반환하는 함수

```js
const animalTypes = ["Lion", "Tiger", "Bear"];
R.map(sightNewAnimal, animalTypes); //=> ["It's a Lion!", "It's a Tiger!", "It's a Bear!"]
```
- 주어진 `animalTypes`의 각각에 해당하는 생성자를 할당하여 객체를 생성하고 해당 객체에서 `sighting` 함수를 실행한 결과를 리스트 형태로 반환한다.

## References
- https://ramdajs.com/docs/#construct
- https://github.com/ramda/ramda/blob/master/test/construct.js
- https://github.com/ramda/types/blob/develop/types/construct.d.ts
