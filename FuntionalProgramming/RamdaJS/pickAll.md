## pickAll
> Similar to pick except that this one includes a key: undefined pair for properties that don't exist.
- pick 함수와 유사하지만, pick 함수에서 제외된 것은 프로퍼티가 존재하지 않을 때 key: undefined 쌍을 (무시하지 않고) 포함하는 것이다.

> See also pick.

### 설명
- `pick`가 오브젝트에서 지정된 키만을 뽑은 오브젝트를 만들지만 오브젝트에 존재하지 않는 키는 결과 오브젝트에서 제외되지만 `pickAll`은 오브젝트에 지정된 키가 존재하지 않더라도 결과 오브젝트에서 키를 제외하지 않고 지정한 키에 undefined 값을 할당한 키-벨류 쌍을 포함한 오브젝트를 생성한다.
- 첫 번재 인자로 반환할 배열에 존재해야 할 키를 나열한다.
- 두 번째 인자로 일부분을 복사하기 위한 대상 오브젝트를 지정한다.
- 반환 값은 첫 번째 인자의 나열한 키를 모두 가진 오브젝트를 반환하지만, 두 번째 인자에 존재하지 않는 키의 경우에는 `undefined` 값을 가진 오브젝트를 반환한다.

### 표현
```
[k] → {k: v} → {k: v}
```
- `[k] →`: 키를 나열한 배열을 받는다.
- `→ {k: v} → `: 키-벨류 쌍이 나열된 오브젝트를 두 번째 인자로 받는다.
- `→ {k: v}`: 두 번째 오브젝트에서 첫 번째 오브젝트에서 나열된 키만를 남긴 오브젝트를 반환하되, 존재하지 않는 키는 제외하도록 한다.

### 예제
```js
R.pickAll(['a', 'd'], {a: 1, b: 2, c: 3, d: 4}); //=> {a: 1, d: 4}
R.pickAll(['a', 'e', 'f'], {a: 1, b: 2, c: 3, d: 4}); //=> {a: 1, e: undefined, f: undefined}
```
- `['a', 'd']` 반환되는 결과 오브젝트에는 

## Reference
- https://ramdajs.com/docs/#pickAll
