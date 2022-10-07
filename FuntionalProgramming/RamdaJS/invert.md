## invert
> Same as R.invertObj, however this accounts for objects with duplicate values by putting the values into an array.

## 표현
```
{s: x} → {x: [ s, … ]}
```
- `{s: x} →` 오브젝트를 받는다. 키가 `s`으로 표기된 것으로 보아 문자열을 받는 것으로 보인다.
- `→ {x: [ s, … ]}` 벨류 `x`가 키가 되고, 키 `s`가 원소가 된다. 키의 중복이 발생하면 단일 키에 배열로 중복되는 값을 나열한다.

## 설명
- 오브젝트를 받아 오브젝트의 프로퍼티명과 해당 프로퍼티의 벨류에 대해 프로퍼티 명은 벨류로 벨류는 프로퍼티명으로 뒤바꾼 결과를 반환한다.
- 뒤바꿀 때 키가 중복된다면 키를 하나로 하고 벨류를 배열 안에 나열한다.

## 예제
```
const raceResultsByFirstName = {
  first: 'alice',
  second: 'jake',
  third: 'alice',
};
R.invert(raceResultsByFirstName);
//=> { 'alice': ['first', 'third'], 'jake':['second'] }
```
- 오브젝트의 프로퍼티명과 해당 프로퍼티의 벨류를 서로 바꾼 결과는
```
{
  'alice' : first,
  'jake' : second,
  'alice' : third,
}
```
- 서로 맞바꾼 결과를 자바스크립트의 오브젝트 포멧에 맞게 바꾸면 프로퍼티 명은 문자열의 벨류가 되고 벨류는 문자열이 아닌 키의 프로퍼티명이 된다.
- 자바스크립트의 프로퍼티명으로 가능한 것은 문자열, 정수, 심볼이므로 키를 문자열로 바꾸어 준다.
```
{
  'alice' : 'first',
  'jake' : 'second',
  'alice' : 'third',
}
```
- 오브젝는 동일한 이름의 프로퍼티를 복수로 가질 수 없으므로 중복되는 프로퍼티명의 벨류는 배열으로 나열한다.
- 일관성을 위해 중복되는 키가 없어 벨류가 하나가 되더라도 배열 안에 나열한다.
```
{
  alice : ['first', 'third'],
  jake : ['second'],
}
```

## Reference
- https://ramdajs.com/docs/#invert
