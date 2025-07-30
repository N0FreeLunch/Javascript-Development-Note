## empty
> Returns the empty value of its argument's type.
- (함수의) 인자의 타입의 빈 값을 반환한다.
> Ramda defines the empty value of Array ([]), Object ({}), String (''), TypedArray (Uint8Array [], Float32Array [], etc), and Arguments.
- Ramda는 빈 값을 배열의 경우 []으로, 오브젝트의 경우 {}으로 문자열의 경우 ''으로, 원소의 타입이 있는 배열인 Uint8Array의 경우 []으로, Float32Array의 경우 [] 등으로 규정한다.
> Other types are supported if they define <Type>.empty, <Type>.prototype.empty or implement the FantasyLand Monoid spec.
- 만약 (어떤 타입의 임의의 값을 <Type>으로 표현할 때) <Type>.empty 프로퍼티가 존재할 때, <Type>.prototype.empty 프로퍼티가 존재할 때, 또는 FantasyLand Monoid spec의 구현일 때, (람다에서 빈 값을 정한 타입이 아닌) 다른 타입도 지원한다.
> Dispatches to the empty method of the first argument, if present.  
- 첫 번째 인자의 empty 메소드가 존재할 때, empty 메소드를 실행한다.

## 설명

- 동일 타입의 빈 값을 반환한다.
- 타입의 빈 값이 정의되어 있는 타입에만 사용 가능하다.

## 문법

```
R.empty(x): *
```
> x
- x: 임의의 값
> Returns *
- (x의 타입과 동일한 타입으로) 임의의 타입 * (으로 나타내는 빈 값)을 반환한다.

## 표현

```
a → a
```
- `a →`: 타입의 임의의 값을 인자로 넣었을 때
- `→ a`: 동일 타입의 빈 값을 반환한다.

## 예제

```js
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

## References
- https://ramdajs.com/docs/#empty
- https://github.com/ramda/ramda/blob/master/test/empty.js
- https://github.com/ramda/types/blob/develop/types/empty.d.ts
