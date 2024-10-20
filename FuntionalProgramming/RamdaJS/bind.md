## bind
> Creates a function that is bound to a context. 
- 컨텍스트의 무언가를 바인딩하고 있는 함수를 생성한다.

> Note: R.bind does not provide the additional argument-binding capabilities of [Function.prototype.bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).
- 자바스크립트 문법의 [`Function.prototype.bind`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)와 달리 `R.bind`는 추가적인 인자를 바인딩하지 않는다.

> See also [partial](./partial.md).

### 설명

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
- `(* → *) →`:
- `→ {*} →`:
- `→ (* → *)`: 

### 예제
```js
const log = R.bind(console.log, console);
R.pipe(R.assoc('a', 2), R.tap(log), R.assoc('a', 3))({a: 1}); //=> {a: 3}
// logs {a: 2}
```
- `R.bind`라는 함수에 로그를 찍는 `console.log`함수와 `console` 오브젝트를 넣어 만든 함수를 log 변수에 넣었다.
- 대상 오브젝트 `{a: 1}`에 `R.assoc('a', 2)` a 프로퍼티에 2를 할당하여 `{a: 2}`가 된다.
- `R.tap(log)`은 전달 받은 `logs {a: 2}`의 값을 log 함수에 넣고 사이드 이펙트로 실행한다. 그래서 `logs {a: 2}`가 콘솔에 찍힌다. 또한 `R.tap`함수는 두 번째 인자로 받은 값을 반환 값으로 그대로 전달한다. 따라서 `R.assoc('a', 3)`의 세 번째 인자로 `{a: 2}`가 전달 된다.
- 전달 받은 `{a: 2}`는 `R.assoc('a', 3)`에 의해 a 프로퍼티에 3을 할당한다.
- 따라서 결과는 `{a: 3}`이 된다.

## Reference
- https://ramdajs.com/docs/#bind
- https://github.com/ramda/ramda/blob/master/test/bind.js
- https://github.com/ramda/types/blob/develop/types/bind.d.ts
