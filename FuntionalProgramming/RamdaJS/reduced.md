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
- 순회 함수의 반환 값으로 사용하여 마지막의 누산 값을 다음 순회 함수 또는 반환 값으로 전달하는 역할을 한다. 보통을 순회 함수로 전달된 누산기 값을 그대로 반환하지만, 변환이 적용된 누산기 값을 인자로 받아 변환된 값을 반환할 수도 있다.
- 순회 함수 내부에서 사용하여 순회 함수의 반환 값으로 사용하므로 다음 순회 함수에 이전의 누산기 값을 전달하기 위해 누산기 값을 그대로 반환을 해야 한다. 따라서 인자로 누산기 값을 전달 받는다.
- 순회 함수를 사용하여 누산기를 다음 순회 함수에 전달하는 계열의 함수에 사용할 수 있다.
- 순회 함수를 적용할 때 원하는 값을 얻었다면 계속적인 순회 함수의 적용을 할 필요가 없을 때가 있다. 이 때 순회 함수의 코드를 동작시켜 리소스를 사용하기 보다는 reduced 함수를 사용하여 순회 함수의 반환 값으로 전달하는 누산기 값을 고정시킬 때 사용한다.
- 어떤 조건을 만족 했을 때의 누산기 값을 도중에 멈추어 최종 결과값까지 전달하게 되므로 결과 값을 예측하기 어려운 블랙 박스가 되어 버린다.

### 표현
```
a → *
```
- `a → `: 첫 번째 인자로 인자 하나를 받는다. 이 때 인자로는 보통 순회 함수의 누산기 값을 전달 받는다.
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
- 먼저 누산기의 초기값인 빈 배열에 `[]` 원소를 추가한다. 배열의 원소 값이 3이하인 경우까지 순회 함수는 순회 함수의 현재 원소를 누산기에 추가하므로 3번째 순회 함수가 반환하는 값은 `[1, 2, 3]`이 된다. 그 다음 부터는 `R.reduced(acc)`가 적용되는데 인자로 받은 값을 그대로 반환한다. 3번째 순회 함수가 반환한 누산기 값을 전달 받아서 동일한 값을 반환하므로 최종 반환값도 `[1, 2, 3]`이 된다.

## Reference
ー https://ramdajs.com/docs/#reduced
