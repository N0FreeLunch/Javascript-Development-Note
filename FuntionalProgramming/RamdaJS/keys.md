## keys
> Returns a list containing the names of all the enumerable own properties of the supplied object. Note that the order of the output array is not guaranteed to be consistent across different JS platforms.

## 표현
```
{k: v} → [k]
```
- `{k: v} →` 첫 번째 인자로 오브젝트를 하나 받는다.
- `→ [k]` 첫 번째 인자로 받은 오브젝트의 모든 키를 원소로 한 배열을 반환한다.

## 설명
- 오브젝트를 받아서 오브젝트의 모든 키를 배열로 반환한다.
- 오브젝트의 키가 자바스크립트의 배열 값이 되기 위해서는 자바스크립트의 여러 타입 중 하나가 되어야 한다. 일반적으로 숫자가 아니라면 문자열이므로 문자열 원소를 가진 배열이 주로 반환된다.

## 예제
```
R.keys({a: 1, b: 2, c: 3}); //=> ['a', 'b', 'c']
```
- `{a: 1, b: 2, c: 3}` 오브젝트의 키는 `a`, `b`, `c`이다. 자바스크립트의 값이어야 배열에 나열할 수 있으므로 이 경우에는 문자열이 되어 결과값은 `['a', 'b', 'c']`이 된다.

## Reference
- https://ramdajs.com/docs/#keys
