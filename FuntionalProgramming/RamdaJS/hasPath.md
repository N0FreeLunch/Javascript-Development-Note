# hasPath

> Returns whether or not a path exists in an object. Only the object's own properties are checked.
- 오즈젝트에 지정한 경로의 프로퍼티가 존재하는지 존재하지 않는지를 반환한다. 단, (프로토타입의 프로퍼티까지는 확인할 수 없고) 주어진 오브젝트가 소유한 프로퍼티들만 확인한다.

## 설명

- 주어진 경로에 해당하는 프로퍼티가 존재하는지 확인한다.
- 첫 번째 인자로 오브젝트의 프로퍼티로 지정할 수 있는 값을 원소로 한 배열을 받늗다. 주어진 오브젝트 뿐만 아니라 주어진 오브젝트 내부에 중첩된(nested) 오브젝트, 곧 프로퍼티에 할당된 오브젝트의 프로퍼티명을 지정할 수 있는 종류가 배열의 원소가 되어야 한다.
- 두 번째 인자로 오브젝트를 받는다.
- 첫 번째 인자로 받은 배열의 원소는 프로퍼티명을 나열한 것이고 나열한 순으로 주어진 오브젝트의 프로퍼티에 접근한다. 다음 원소는 프로퍼티의 오브젝트 내부의 프로퍼티에 접근한다.
- 배열로 지정한 경로로 오브젝트의 프로퍼티의 프로퍼티의 프로퍼티를 접근하여 최종 경로까지의 프로퍼티가 존재하면 참을 아니면 거짓을 반환한다.

## 문법

```
R.hasPath(path, obj)
```
> `path`: The path to use.
- `path`: 사용할 경로
> `obj`: The object to check the path in.
- `obj`: 경로에 (대상 프로퍼티가 존재하는지) 확인할 오브젝트
> Returns Boolean Whether the path exists.
- 불리언을 반환한다. 경로가 존재하는지 (하지 않는지를 나타내는 불리언)

## 표현

```
[Idx] → {a} → Boolean
Idx = String | Int | Symbol
```
- `Idx = String | Int | Symbol`: 인덱스는 문자열, 수, 심볼 형태로만 받을 수 있다. 이는 오브젝트의 프로퍼티로 지정할 수 있는 종류가 이 종류 밖에 없기 때문
- `[Idx] →`: 첫 번째 인자로 오브젝트의 프로퍼티로 지정할 수 있는 값을 배열 형태로 나열한다. 프로퍼티의 깊이에 따라 배열에 원소를 나열한다.
- `→ {a} →`: 두 번째 인자로 오브젝트를 받는다.
- `→ Boolean`: 첫 번째 인자의 배열에 나열한 원소순으로 주어진 오브젝트의 프로퍼티를 접근하고 배열에 나열된 모든 프로퍼티를 접근할 수 있다면 참 아니면 거짓을 반환한다.

## 예제

```js
R.hasPath(['a', 'b'], {a: {b: 2}});         // => true
R.hasPath(['a', 'b'], {a: {b: undefined}}); // => true
R.hasPath(['a', 'b'], {a: {c: 2}});         // => false
R.hasPath(['a', 'b'], {});                  // => false
```

## Referneces

- https://ramdajs.com/docs/#hasPath
- https://github.com/ramda/ramda/blob/master/test/hasPath.js
- https://github.com/ramda/types/blob/develop/types/hasPath.d.ts
