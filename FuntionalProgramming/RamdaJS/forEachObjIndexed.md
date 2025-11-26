## forEachObjIndexed

> iterate over an input object, calling a provided function fn for each key and value in the object.
- input object를 순회한다. 제공된 함수를 fn이라고 할 때, 이 함수는 각각의 키와 값을 (인자로) 받아 호출한다.
> fn receives three argument: (value, key, obj).
- (첫 번째 인자로 받는 함수인) fn은 세 인자를 받는데 (value, key, obj)이다.

## 설명

- `forEach`가 배열을 
- 첫 번째 인자로 두 개의 인자를 받는 함수를 받는다.
- 두 번째 인자로 오브젝트 받는다.
- 첫 번째 인자로 받은 함수의 인자에 두 번째 인자로 받은 오브젝트의 키-벨류 쌍을 하나씩 할당하여 첫 번째 인자로 받은 함수를 실행한다.
- 이 때 첫 번째 인자에 할당된 함수는 키-벨류 순서가 아닌 아닌 벨류-키 순서로 인자를 받는다.
- 오브젝트가 가지고 있는 프로퍼티 갯수 만큼 키-벨류 쌍을 함수에 할당하기 때문에 프로퍼티 갯수만큼 순회한다.

## 문법

```
R.forEachObjIndexed(fn, obj): Object
```
> `fn`: The function to invoke. Receives three argument, value, key, obj.
- `fn`: 호출할 함수. value, key, obj 세 개의 함수를 받는다.
> `obj`: The object to iterate over.
- `obj`: 순회할 오브젝트
> Returns Object The original object.
- Object를 반환하는데, 원본 오브젝트를 반환하므로 Object가 반환된다.

## 표현

```
((a, String, StrMap a) → Any) → StrMap a → StrMap a
```
- `((a, String, StrMap a) → Any) →`: 인자로 벨류를 받으므로 어떤 타입 `a`를 받고, 프로퍼티명을 받으므로 문자열로 받고, 
- `→ StrMap a →`: 두 번째 인자로 프로퍼티명이 문자열 이루어진 문자열 프로퍼티 맵을 받는다. 문자열 프로퍼티명으로 이루어진 오브젝트 형식도 여기에 할당 할 수 있다.
- `→ StrMap a`: `forEach` 함수와 마찬가지로 반환 함수는 두 번째 인자로 들어온 대상을 그대로 반환한다.


## 예제

```js
const printKeyConcatValue = (value, key) => console.log(key + ':' + value);
R.forEachObjIndexed(printKeyConcatValue, {x: 1, y: 2});  //=> {x: 1, y: 2}
// logs x:1
// logs y:2
```
- `(value, key) => console.log(key + ':' + value)` 벨류와 키를 받아서 이를 `console.log`로 해당 값을 콘솔 창에 표시한다.
- `printKeyConcatValue` 첫 번째 순회엣 함수에 첫 번째 인자로 1, 두 번째 인자로 'x'를 할당하고 두 번째 순회에 첫 번째 인자로 2, 두 번째 인자로 'x'를 할당한다.

## References

- https://ramdajs.com/docs/#forEachObjIndexed
- https://github.com/ramda/ramda/blob/master/test/forEachObjIndexed.js
- https://github.com/ramda/types/blob/develop/types/forEachObjIndexed.d.ts
