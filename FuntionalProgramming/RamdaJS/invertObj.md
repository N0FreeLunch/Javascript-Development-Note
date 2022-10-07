## invertObj
> Returns a new object with the keys of the given object as values, and the values of the given object, which are coerced to strings, as keys. 
- 주어진 오브젝트의 키를 값으로 하고, 주어진 오브젝트의 값(values)은 문자열로 강제 변환된 키로 구성된 새로운 오브젝트를 반환합니다.

> Note that the last key found is preferred when handling the same value.
- 같은 값을 처리할 때는 가장 마지막 키를 우선시한다.

## 표현
```
{s: x} → {x: s}
```
- `{s: x} →` 인자로 오브젝트를 받는다.
- `→ {x: s}` 첫 번째 인자의 오브젝트의 키와 벨류가 서로 바뀐 오브젝트가 반환된다.


## 섦명
- `invert`가 오브젝트의 프로퍼티명과 해당 벨류의 위치를 바꾸고 중복 키를 단일하게 하면서 벨류를 배열로 나열한 것에 반해, `invertObj`는 키 중복이 일어나더라도 오브젝트의 프로퍼티를 순차적으로 처리하면서 중복 키가 생기는 경우네는 가장 마지막에 처리된 키와 그 벨류 값으로 지정되어 반환된다.
- 첫 번째 인자로 오브젝트 또는 배열을 받는다.
- 받은 오브젝트 내부의 키와 벨류의 위치를 서로 바꾼 새로운 오브젝트를 반환한다.
- 자바스크립트의 배열은 인덱스가 수로 이루어진 오브젝트이므로 배열을 받게 되면 벨류로 수가 형변환 된 문자열이 된 값이 나온다.

## 예제
```
const raceResults = {
  first: 'alice',
  second: 'jake'
};

R.invertObj(raceResults);
//=> { 'alice': 'first', 'jake':'second' }

// Alternatively:
const raceResults = ['alice', 'jake'];
R.invertObj(raceResults);
//=> { 'alice': '0', 'jake':'1' }
```
- `{ first: 'alice', second: 'jake' };` 주어진 오브젝트의 키 벨류의 위치를 바꾼다. 자바스크립트에서 오브젝트의 키는 문자열으로 변환된다. 따라서 `{ 'alice': 'first', 'jake':'second' }`가 된다.
- `['alice', 'jake']` 배열을 인자로 넣은 경우 `{ 0: 'alice', 1: 'jake' }`과 유사한 오브젝트가 된다.
- 오브젝트의 키-벨류의 위치를 서로 바꾸고 정수 키는 문자열으로 변환되어 벨류가 된다. `{ 'alice': '0', 'jake':'1' }`가 된다.


## Reference
- https://ramdajs.com/docs/#invertObj
