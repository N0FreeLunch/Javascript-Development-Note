## bind

> Creates a function that is bound to a context. 
- 컨텍스트의 무언가를 바인딩하고 있는 함수를 생성한다.

> Note: R.bind does not provide the additional argument-binding capabilities of [Function.prototype.bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).
- 자바스크립트 문법의 [`Function.prototype.bind`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)와 달리 `R.bind`는 추가적인 인자를 바인딩하지 않는다.

> See also [partial](./partial.md).

### 설명

- 자바스크립트의 bind가 첫 번째 인자로는 실행 환경이 되는 오브젝트를 받고, 두 번째 인자부터 차례로 함수의 첫 번째, 두 번째 ... 인자를 바인딩하는 것과 달리, Ramda의 R.bind는 실행할 함수와 실행 된경이 되는 오브젝트를 인자로 받지만, 인자를 바인딩하지는 않는다. Rmada에서는 커링을 통해 인자를 바인딩 할 수 있기 때문에 자바스크립트의 bind와 같이 인자를 바인딩할 필요가 없다.

#### 자바스크립트에서의 [Function.prototype.bind()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

자바스크립트의 bind 메소드는 function 키워드를 사용한 함수에 사용할 수 있다.

```js
const module = {
  x: 42,
  getX: function () {
    return this.x;
  },
};

const unboundGetX = module.getX;

const boundGetX = unboundGetX.bind(module);
```
- `console.log(module.getX)`: `function () { return this.x; }` 함수가 실행된다.
- `console.log(module.getX())`: 자바스크립트에서 `this`는 함수를 실행하는 시점에서의 `this`를 둘러싸고 있는 오브젝트에 접근을 한다. 이를 렉시컬 스코프라고한다. `module.getX()`는 `modele` 오브젝트 내부의 `getX`라는 메소드를 실행하므로 `this`의 렉시컬 스코프는 `module` 오브젝트가 된다. `module` 오브젝트에 바인딩 된 `x`키를 `this.x`란 코드를 통해서 가져온다.
- `console.log(unboundGetX)`: `function () { return this.x; }` 함수가 실행된다.
- `console.log(unboundGetX())`:  자바스크립트에서 `this`는 함수를 실행하는 시점에서의 `this`를 둘러싸고 있는 오브젝트에 접근을 하는데, 이를 렉시컬 스코프라고한다. `module.getX()`와 달리 `unboundGetX`는 `module` 오브젝트 내부의 `getX`가 아닌, window 오브젝트 내부의 `function () { return this.x; }` 함수가 실행된다. `this`의 렉시컬 스코프는 `window` 오브젝트가 된다. `this`가 가리키는 대상은 `window` 오브젝트가 되고, `window` 오브젝트에 x 프로퍼티가 정의되어 있지 않기 때문에 `undefined`가 반환된다.
- `console.log(boundGetX())`: `boundGetX` 함수에 `module`이란 둘러싸고 있는 환경을 지정하면, `boundGetX`는 `module` 오브젝트의 환경 안에서 실행된다. `boundGetX` 함수에는 `module` 오브젝트 환경이 바인딩되어 있기 때문에 `function () { return this.x; }`의 코드를 실행할 때 `this`는 `module` 오브젝트를 가리키게 되고, `this.x`는 `module`의 프로퍼티 `x`에 접근하게 된다.

```js
function addArguments(arg1, arg2) {
  return arg1 + arg2;
}

var result1 = addArguments(1, 2); // 3

var addThirtySeven = addArguments.bind(null, 37);

var result2 = addThirtySeven(5); // 37 + 5 = 42

var result3 = addThirtySeven(5, 10); // 37 + 5 = 42
```
- `func.bind(thisArg[, arg1[, arg2[, ...]]])` 바인드 메소드의 두 번째 인자 부터는 첫 번째 인자에 바인딩할 값, 두 번째 인자에 바인딩 할 값 ... 이런식으로 인자에 값을 바인딩할 수 있다. `addArguments.bind(null, 37)`의 코드는 첫 번째 인자로 37의 인자에 바인딩한다는 의미이다.
- 첫 번째 인자에 값이 바인딩 되어 있으므로, 함수는 바인딩된 인자는 받지 않고 그 다음 인자부터 받는다. 인자가 바인딩 되기 전의 `addThirtySeven(37, 5)`는 바인딩 된 이후의 `addThirtySeven(5)`가 되고, 바인딩 되기 전의 `addThirtySeven(37, 5)`는 바인딩 된 이후의 `addThirtySeven(5, 10)`으로 나타낸다. 바인딩 된 이후의 인자 5는 바인딩 되기 전의 두 번째 인자가 되고, 바인딩 된 이후의 인자 10은 바인딩 도기 전의 세 번째 인자가 된다. 인자가 바인딩 되기 전의 `addThirtySeven`는 첫 번째 인자와 두 번째 인자만을 처리하기 때문에, 세 번째 인자는 처리하지 않게 된다.

### 문법
```
R.bind(fn, thisObj): function
```
- fn: The function to bind to context
- thisObj: The context to bind fn to
- Returns function A function that will execute in the context of `thisObj`.

### 표현
```
(* → *) → {*} → (* → *)
```
- `(* → *) →`: 첫 번째 인자로 실행할 함수를 받는다.
- `→ {*} →`: 두 번째 인자로 함수의 실행 환경 오브젝트를 받는다.
- `→ (* → *)`: 반환된 함수는 첫 번째 인자로 받은 함수와 동일한 코드를 실행하지만, 두 번째 인자로 받은 오브젝트에 감싸인 환경에서 실행된다. 따라서 두 번째 인자로 받은 오브젝트의 프로퍼티를 첫 번째로 받은 함수에서 `this.`을 통해 접근할 수 있다.

### 예제
```js
const log = R.bind(console.log, console);
R.pipe(R.assoc('a', 2), R.tap(log), R.assoc('a', 3))({a: 1}); //=> {a: 3}
// logs {a: 2}
```
- `R.bind`라는 함수에 로그를 찍는 `console.log`함수는 `console`이란 오브젝트 환경에서 `log` 프로퍼티가 갖는 코드가 실행된다. `R.bind(console.log, console)`는 `console.log`의 코드를 실행하는 환경을 `console` 오브젝트로 감싼 환경을 설정하는 것이다. 따라서 `log` 함수는 `console.log`의 코드를 실행하되, 코드가 실행될 환경을 `console` 오브젝트로 한다.
- 대상 오브젝트 `{a: 1}`에 `R.assoc('a', 2)`로 a 프로퍼티에 2를 할당하여 `{a: 2}`가 된다.
- `R.tap(log)` 사이드 이펙트로 `log` 함수를 실행한다. 전달 받은 `{a: 2}`의 값을 `log` 함수의 인자로 넣어 사이드 이펙트로 실행한다. `tap` 함수는 사이드 이펙트로 인자로 받은 함수에 인자로 받은 값을 전달해 사이드 이펙트를 실행하고 전달 받은 값을 그대로 받환한다. `{a: 2}`는 사이드 이펙트로 콘솔에 찍히고 그 값이 그 대로 반환되어 따라서 `R.assoc('a', 3)`는 세 번째 인자로 `{a: 2}`를 전달 받는다.
- 전달 받은 `{a: 2}`는 `R.assoc('a', 3)`에 의해 a 프로퍼티에 3을 할당한다. 따라서 결과는 `{a: 3}`이 된다.

## References
- https://ramdajs.com/docs/#bind
- https://github.com/ramda/ramda/blob/master/test/bind.js
- https://github.com/ramda/types/blob/develop/types/bind.d.ts
