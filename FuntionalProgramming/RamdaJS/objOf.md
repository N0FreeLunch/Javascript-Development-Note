## objOf
> Creates an object containing a single key:value pair.
- 하나의 키:벨류 쌍을 갖는 하나의 오브젝트를 생성한다.

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

## Reference
- https://ramdajs.com/docs/#objOf
