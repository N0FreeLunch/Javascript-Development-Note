## objOf
> Creates an object containing a single key:value pair.
- 하나의 키:벨류 쌍을 갖는 하나의 오브젝트를 생성한다.

> See also pair.

## 설명
- 첫 번째 인자로 오브젝트의 키로 세팅할 문자열 값을 하나 받고, 두 번째 인자로 첫 번째 인자의 키에 할당할 값을 하나 받는다.
- 두 인자를 받아서 첫 번째 인자를 키로, 두 번째 인자를 키의 값으로 하는 리터럴 오브젝트를 반환한다.
- 반환된 결과는 한 쌍의 키-벨류를 갖는 리터럴 오브젝트가 된다.

## 표현
```
String → a → {String:a}
```
- `String →` 첫 번째 인자로 문자열을 받는다.
- `→ a →` 두 번째 임의의 타입의 값을 받는다.
- `→ {String:a}` 첫 번째 인자를 키로, 두 번째 인자를 값으로 하는 오브젝트를 반환한다.

## 예제
```js
const matchPhrases = R.compose(
  R.objOf('must'),
  R.map(R.objOf('match_phrase'))
);
matchPhrases(['foo', 'bar', 'baz']); //=> {must: [{match_phrase: 'foo'}, {match_phrase: 'bar'}, {match_phrase: 'baz'}]}
```
- `R.compose`는 오른쪽 함수의 결과를 왼쪽 함수의 인자로 받는 절차를 수행한다. `compose(f,g)(x)`의 의미는 `f(g(x))`가 된다.
- 위의 예제는 아래에서 위로 함수를 합성한다. `(R.objOf('must'))(R.map(R.objOf('match_phrase'))((['foo', 'bar', 'baz'])))`가 되는 꼴이다.
- 합성된 함수에 인자를 넣어 평가가 되는 과정은 `R.map(R.objOf('match_phrase'))`는 `['foo', 'bar', 'baz']`의 각각의 원소에 `R.objOf('match_phrase')`를 적용하는 것이다. 따라서 `[{"match_phrase": "foo"}, {"match_phrase": "bar"}, {"match_phrase": "baz"}]`가 된다. 이 결과에 `R.objOf('must')`를 적용하므로 `{must: [{match_phrase: 'foo'}, {match_phrase: 'bar'}, {match_phrase: 'baz'}]}`라는 결과가 나온다.

## Reference
- https://ramdajs.com/docs/#objOf
