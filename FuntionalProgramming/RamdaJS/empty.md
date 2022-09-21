## empty
> Returns the empty value of its argument's type. Ramda defines the empty value of Array ([]), Object ({}), String (''), TypedArray (Uint8Array [], Float32Array [], etc), and Arguments. Other types are supported if they define <Type>.empty, <Type>.prototype.empty or implement the FantasyLand Monoid spec.

> Dispatches to the empty method of the first argument, if present.  

## 표현
```
a → a
```
- `a →` 타입의 임의의 값을 인자로 넣었을 때
- `→ a` 동일 타입의 빈 값을 반환한다.

## 설명
- 동일 타입의 빈 값을 반환한다.
- 타입의 빈 값이 정의되어 있는 타입에만 사용 가능하다.

## 예제
```
R.empty(Just(42));               //=> Nothing()
R.empty([1, 2, 3]);              //=> []
R.empty('unicorns');             //=> ''
R.empty({x: 1, y: 2});           //=> {}
R.empty(Uint8Array.from('123')); //=> Uint8Array []
```
- `[1, 2, 3]` 배열이다. 배열의 빈 값은 빈 배열이라서 `[]`
- `'unicorns'` 문자열이다. 문자열의 빈 값은 빈 문자열이라서 `''`
- `{x: 1, y: 2}` 오브젝트이다. 오브젝트의 빈 값은 빈 오브젝트라서 `{}`
- `Uint8Array.from('123')` `Uint8Array` 함수는 8-bit unsigned integer를 바이너리 데이터를 배열로 다룰 수 있는 메모리 버퍼를 제공하는 함수이다. 이 배열이 제공하는 빈 값에 해당하는 배열이 반환되므로 `Uint8Array` 타입의 빈 배열 `[]`이 반환된다.

## Reference
- https://ramdajs.com/docs/#empty
