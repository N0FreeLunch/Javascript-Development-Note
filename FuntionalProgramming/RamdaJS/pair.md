## pair
> Takes two arguments, fst and snd, and returns [fst, snd].
- 두 인자 fst와 snd를 받아서, `[fst, snd]`를 반환한다.

> See also objOf, of.

### 설명
- 두 개의 인자를 받아서 두 값이 있는 배열을 반환하는 함수를 `R.curry((a, b) => [a, b])` 직접 만들면 되는데 굳이 만들 필요가 있을까를 생각하게 하는 함수이다.
- 만약 인자를 무한정 받을 수 있고, 그 인자 리스트의 배열을 반환한다고 하면, 커링을 어떻게 구성할지 모호한 문제가 있다. 그래서 제한된 인자로 배열을 반환하는 코드를 만드는 것이 중요하다.
- [pair 함수를 제안한 문서](https://github.com/ramda/ramda/issues/1310)를 보면 2개의 인자를 받는 것은 유의미한 기능을 갖는다.

### 표현 
```
a → b → (a,b)
```
- `a → ` 첫 번째 인자를 받는다. 이때 첫 번째 인자를 a라고 하자.
- `→ b →` 두 번째 인자를 받는다. 이때 두 번째 인자를 b라고 하자.
- `→ (a,b)` 첫 번째 인자와 두 번째 인자 쌍을 반환한다. 인자로 받은 a, b를 그대로 반환한다.

### 예제
```js
R.pair('foo', 'bar'); //=> ['foo', 'bar']
```
- 두 인자 `'foo'`, `'bar'`를 받아서 `['foo', 'bar']`를 반환한다.

## Reference
- https://ramdajs.com/docs/#pair
- https://github.com/ramda/ramda/issues/1310
