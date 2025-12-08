# identity

> A function that does nothing but return the parameter supplied to it. Good as a default or placeholder function.
- 아무것도 하지 않는 함수이다. 파라메터로 주어진 값을 그대로 반환하는 함수이다. 디폴드 함수를 넣을 때 또는 함수를 플레이스 홀더용 용도로 사용할 때 좋다.

## 설명

- 인자의 값을 그대로 반환하는 함수이다.
- 오브젝트의 경우는 동일한 참조를 반환한다.

## 문법

```
R.identity(x): *
```

> `x`: The value to return.
- `x`: 반환할 값
> Returns * The input value, `x`.
- 어느 타입이든 반환한다. (인자로) 입력된 값을 (그대로).

## 표현

```
a → a
```

- `a →`: 넣은 인자를
- `→ a`: 그대로 반환한다. (그래서 종류도 동일하다)

## 예제

```js
R.identity(1); //=> 1

const obj = {};
R.identity(obj) === obj; //=> true
```

## References

- https://ramdajs.com/docs/#identity
- https://github.com/ramda/ramda/blob/master/test/identity.js
- https://github.com/ramda/types/blob/develop/types/identity.d.ts
