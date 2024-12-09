## dec
> Decrements its argument.

### 설명

- Number값을 받아서 값을 1 감소시킨다.

### 문법 

```
R.dec(n): Number
```
> `n`
- `n`: 인자 n에 대하여
> Returns Number n - 1
- `n - 1`을 계산한 수를 반환한다.

### 표현

```
Number → Number
```
- `Number →`: 첫 번째 인자로 수를 받는다.
- `→ Number`: 인자로 받은 수에서 1을 뺀 값을 반환한다.

### 예제
```js
R.dec(42); //=> 41
```
- 수 42를 받아서 1을 감소 시킨 결과값을 반환한다.

## References

- https://ramdajs.com/docs/#dec
- https://github.com/ramda/ramda/blob/master/test/dec.js
- https://github.com/ramda/types/blob/develop/types/dec.d.ts
