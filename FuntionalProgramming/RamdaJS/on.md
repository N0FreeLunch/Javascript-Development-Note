## on
> Takes a binary function f, a unary function g, and two values. Applies g to each value, then applies the result of each to f.
- 인자를 두 개 받는 함수 f, 인자를 하나 받는 함수 g, 그리고 두 값을 받아서, 인자를 하나 받는 함수에 받은 두 값을 각각 적용하고, 각각의 결과 값을 인자를 두 개 받는 함수에 적용한다.

> Also known as the P combinator.

### 설명


### 표현
```
((a, a) → b) → (c → a) → c → c → b
```

### 예제
```js
const eqBy = R.on((a, b) => a === b);
eqBy(R.prop('a'), {b:0, a:1}, {a:1}) //=> true;

const containsInsensitive = R.on(R.includes, R.toLower);
containsInsensitive('o', 'FOO'); //=> true
```
- `R.on` 함수는 `(a, b) => a === b` 인자를 두 개 받는 함수를 첫 번째 인자로 받는다.
- `R.on` 함수는 두 번째 인자로 오브젝트를 인자로 받으면 오브젝트의 `a`라는 키의 값을 추출해 주는 인자를 하나 받는 함수 `R.prop('a')`를 받는다.
- `R.on` 함수는 세 번째 인자와 네 번째 인자로 `{b:0, a:1}`와 `{a:1}`를 각각 받는다.
- `{b:0, a:1}`와 `{a:1}` 각각에 `R.prop('a')`를 적용하면 `R.prop('a')({b:0, a:1})` 와 `R.prop('a')({a:1})`가 된다. 결과 값은 각각 `1`과 `1`이 된다.
- 이 평가 결과를 첫 번째로 받는 인자인 함수 `(a, b) => a === b`에 전달하면 `1 === 1`이므로 결과는 `true`가 된다.

## Reference
- https://ramdajs.com/docs/#on
