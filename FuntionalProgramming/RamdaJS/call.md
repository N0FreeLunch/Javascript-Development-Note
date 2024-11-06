## call

> Returns the result of calling its first argument with the remaining arguments.
- (첫 번재 인자가 아닌) 나머지 인자로 (함수인) 첫 번째 인자를 호출한 결과를 반환한다.

> This is occasionally useful as a converging function for R.converge: the first branch can produce a function while the remaining branches produce values to be passed to that function as its arguments.
- 이 함수는 [R.converge](./converge.md)의 수렴 함수로서 유용하다. R.converge는 (첫 번째 인자로 수렴 함수를, 두 번째 인자로 분기 함수 리스트를 받아, 리스트의 분기 함수 각각의 평가 결과를 수렴 함수의 인자로 전달하는데) 첫 번째 분기로 (인자를 받아 반환 값으로) 함수를 생성할 수 있고, 나머지 분기는 해당 함수에 인수로 전달될 값을 (인자를 받아 반환 값으로) 생성합니다. (그리고 생성된 값을 수렴 함수로 전달한다.)

> See also [apply](./apply.md).

### 설명
- 첫 번째 인자로 함수를 받고, 나머지 인자로 첫 번째 인자로 받은 함수에 전달할 인자 값을 받아서, '첫 번째 인자'(나머지 인자들) 꼴로 함수를 호출한다.
- 수렴 함수에 적용하기 좋다는 의미는 `R.converge(R.call, [함수를 반환하는 함수, 값을 반환하는 함수...])`의 형태로 쓰면, '함수를 반환하는 함수'에 의해 '반환된 함수'와 '값을 반환하는 함수 1', '값을 반환하는 함수 2', '값을 반환하는 함수 3'...에 의해 반환된 값1, 값2, 값3...이 다음과 같이 할당이 된다. `R.call(반환된 함수, 값1, 값2, 값3 ...)` 이 결과는 `'반환된 함수'(값1, 값2, 값3 ...)`의 형태가 되기 때문에 `R.converge`의 수렴 함수로 `R.call`이 유용하다는 의미이다.

### 문법
```
R.call(fn, args): *
```
> `fn`: The function to apply to the remaining arguments.
- `fn`: 남은 인자들(첫 번째 인자를 제외한 나머지로 두 번째 인자부터 마지막 인자까지)을 적용할 함수이다.
> `args`: Any number of positional arguments.
- `args`: 어떠한 갯수든지 (첫 번째 함수에 인자 전달할 순서를 정하는) '나열된 순서대로 전달하기 위한'(positional) 인자들
> Returns *
- (fn에 인자를 전달한 결과로써 fn의 반환 타입에 따라 달라지므로 어떠한 타입이라도 가능한) * 

### 표현
```
((*… → a), *…) → a
```
- `((*… → a), *…) →`: 두 개 이상의 인자를 동시에 받아야 한다. 첫 번째 인자로 `(*… → a)`로 함수를 받고, 두 번째 인자 부터는 첫 번째 인자의 함수에 전달할 값 `*…`을 받는다. 두 번째 인자부터 마지막 인자까지의 모든 인자는 첫 번째 인자로 받는 함수의 인자에 할당할 수 있는 종류의 값을 받아야 한다.
- `→ a`: 첫 번째 인자로 받은 `(*… → a)` 함수의 결과를 반환한다. 이는 `(*… → a)` 함수에 두 번째 인자 부터 마지막 인자까지의 `*…`를 인자로 전달해서 얻은 결과값이므로 `(*… → a)`의 반환 값과 동일한 `a`종류의 값을 반환한다.

### 예제
```js
R.call(R.add, 1, 2); //=> 3
```
- `R.call(R.add, 1, 2);` `R.call`이란 함수는 첫 번째 인자로 함수를 받고, 두 번째 인자 부터는 첫 번째 인자로 받은 함수의 인자로 집어 넣을 인자를 받는다. `R.add`에 인자 `1`과 `2`를 넣는다는 뜻이다.

```js
const indentN = R.pipe(
  R.repeat(' '),
  R.join(''),
  R.replace(/^(?!$)/gm)
);

const format = R.converge(
  R.call,
  [
    R.pipe(R.prop('indent'), indentN),
    R.prop('value')
  ]
);

format({indent: 2, value: 'foo\nbar\nbaz\n'}); //=> '  foo\n  bar\n  baz\n'
```
- `R.repeat(' ')` 는 원소가 배열에서 `' '`라는 동일한 원소를 지정한 수 만큼을 넣은 배열을 만든다.
- `R.join('')`은 배열의 원소 사이를 `''`으로 연결한 단일 문자열으로 만든다.
- `R.replace(/^(?!$)/gm)`는 문자열 맨 앞에 매칭(`^`)하며, 문자열의 마지막(`$`)이 아닌 값(`(?!$)`)을 입력된 값으로 치환하겠다는 의미이다. ([Assertions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Assertions)에서 `x(?!y)`를 검색하자.) 곧, 빈 문자열이 아니라 어떠한 문자라도 있다면 해당 문자열의 맨 앞을 어떤 값으로 치환한다는 의미를 가진다.
- `R.pipe`는 왼쪽에서 오른쪽으로 함수를 합성하므로 `indentN(N)`은 `R.replace(/^(?!$)/gm)(R.join('')(R.repeat(' ')(N)))`의 꼴로 실행 된다. 공백문자 `' '`를 N개 나열한 배열을 `R.join('')`으로 묶어 N개의 공백을 가진 문자를 만든다. 그리고 이 문자열을 입력 받은 문자열이 공백이 아닐 때 맨 앞의 문자열을 공백문자가 N개 나열된 문자열로 바꾼다는 의미를 갖는다.
- `R.pipe(R.prop('indent'), indentN)`는 오브젝트를 하나 받아서 프로퍼티 `indent`의 값을 뽑아 `indentN`의 N을 지정하겠다는 의미로 어떤 문자열을 받아 오브젝트의 `indent`의 값 만큼 들여쓰기 공백 문자를 추가하겠다는 의미이다.
- `R.converge(R.call,[R.pipe(R.prop('indent'), indentN),R.prop('value')])`는 `{indent: 2, value: 'foo\nbar\nbaz\n'}`에서 value 프로퍼티 값인 `'foo\nbar\nbaz\n'`을 뽑아서 2개의 공백 만큼 들여쓰기를 하여 `'  foo\n  bar\n  baz\n'`라는 결과를 얻는다.

## References
- https://ramdajs.com/docs/#call
- https://github.com/ramda/ramda/blob/master/test/call.js
- https://github.com/ramda/types/blob/develop/types/call.d.ts
