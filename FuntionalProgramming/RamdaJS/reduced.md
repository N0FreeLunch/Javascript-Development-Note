## reduced
> Returns a value wrapped to indicate that it is the final value of the reduce and transduce functions. The returned value should be considered a black box: the internal structure is not guaranteed to be stable.
- reduce와 transduce 함수의 마지막 값을 레핑한(wrapped) 값을 반환한다. 반환된 값은 (함수) 내부의 값은 안정성이 보장되지 않은 블랙 박스로 고려되어야 한다.

> This optimization is available to the below functions:
- 이 최적화는 다음 함수에 사용할 수 있다.

> reduce
> reduceWhile
> reduceBy
> reduceRight
> transduce

> See also reduce, reduceWhile, reduceBy, reduceRight, transduce.

### 설명

### 표현
```
a → *
```
- `a → `: 첫 번째 인자로 인자 하나를 받는다.
- `→ *`: 내부의 동작을 알 수 없는 블랙박스의 함수이므로 어떤 값이 반환될지 알 수 없다.

### 예제
```js
R.reduce(
 (acc, item) => item > 3 ? R.reduced(acc) : acc.concat(item),
 [],
 [1, 2, 3, 4, 5]) // [1, 2, 3]
```
- `R.reduce` 함수의 첫 번째 인자는 순회 함수를 받고, 두 번째 인자로 누산기의 초기값을 받으며, 세 번째 인자로 순회할 배열을 받는다.
- 순회 함수는 첫 번째 인자로 누산기를 받고, 누 번째 인자로 순회 대상 (배열의) 원소를 전달 받는다. 그런데 순회 함수의 반환 값으로 누산기 값을 받는 `R.reduced(acc)`를 적용하였다. 순회 대상 원소가 3보다 클 때 `R.reduced(acc)`를 적용하고, 순회 대상 원소가 3과 같거나 작을 때 `acc.concat(item)`으로 누산기 배열에 순회 함수의 대상 현재 처리 원소를 추가한다.

## Reference
ー https://ramdajs.com/docs/#reduced
