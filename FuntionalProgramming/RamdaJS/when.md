## when
> Tests the final argument by passing it to the given predicate function.
- 마지막 인자가 주어진 술어함수를 통과하는지를 테스트한다.
> If the predicate is satisfied, the function will return the result of calling the whenTrueFn function with the same argument.
- 술어함수를 만족하지 못한다면, 술어함수의 결과가 true를 반환했을 때 실행하는 함수(whenTrueFn)를 (when 함수가 받은 인자와) 동일한 인자를 전달하여 호출한 결과를 반환한다.
> If the predicate is not satisfied, the argument is returned as is.
- 술어함수가 만족되지 않는다면, (when 함수가 받은) 인자를 그대로 반환한다.

> See also [ifElse](./ifElse.md), [unless](./unless.md), [cond](./cond.md).

### 설명
- unless가 술어함수를 만족하지 못했을 때 주어진 함수를 실행한 결과를 반환하고 술어함수를 만족했을 때 전달된 값을 그대로 반환하는 것과 달리 것과 달리, when은 술어함수의 결과에 대해 반대로 적용된다. 술어함수를 만족했을 때 주어진 함수를 실행한 결과를 반환하고 술어함수를 만족하지 못했을 때 전달된 값을 그대로 반환한다.

### 표현
```
(a → Boolean) → (a → b) → a → a | b
```
- `(a → Boolean) →`: 첫 번째 인자로 술어 함수를 받는다. 이 술어함수는 인수로 세 번째 인자의 값을 받으므로 a 타입 파라메터를 갖는다.
- `→ (a → b) →`: 두 번째 인자로 첫 번째 인자로 받은 술어함수의 평가 결과가 참일 때 최종 반환할 값을 결정하기 위한 함수를 받는다. 세 번째 인자로 받은 값을 전달 받으므로 a 타입 파라메터를 갖는다.
- `→ a →` : 세 번째 인자로 첫 번째 인자로 받은 함수의 인자로 전달할 값을 받는다. 이 값을 첫 번째 인자로 받은 함수에 전달 했을 때, 함수가 반환하는 참 거짓의 결과에 따라 참이면 두 번째 인자로 받는 함수의 인자로 값을 전달한다.
- `→ a | b`: 최종 반환 값은 세 번째로 받은 인자가 술어함수를 만족하지 못할 때는 세 번째 인자 그대로의 값을 반환하므로 a 타입 파라메터를 가지며, 술어함수를 만족했을 때는 두 번째 인자로 받은 함수의 반환값의 타입 파라메터인 b를 가진다.

### 예제
```js
// truncate :: String -> String
const truncate = R.when(
  R.propSatisfies(R.gt(R.__, 10), 'length'),
  R.pipe(R.take(10), R.append('…'), R.join(''))
);
truncate('12345');         //=> '12345'
truncate('0123456789ABC'); //=> '0123456789…'
```
- `R.propSatisfies(R.gt(R.__, 10), 'length')`는 술어함수에 해당한다. `propSatisfies` 함수는 어떤 인자를 받아 그 값이 10보다 큰지를 확인하는 `R.gt(R.__, 10)` 함수를 받으며, 오브젝트를 받아 오브젝트에서 `'length'` 프로퍼티의 값을 술어함수에 전달하여 참, 거짓을 판단한다.
- 술어함수를 만족했을 때 `R.pipe(R.take(10), R.append('…'), R.join('')` 함수에 `truncate('12345')`이라면 `'12345'`를 전달하여 반환된 결과를 최종 반환하고, `truncate('0123456789ABC')`이라면 `'0123456789…'`를 전달하여 반환된 결과를 반환한다.
- 술어함수를 만족하지 못했을 때 `truncate('12345')`이라면 `'12345'`를 반환하고, `truncate('0123456789ABC')`이라면 `'0123456789…'`를 반환한다.
- `truncate('12345')`는 문자열의 길이가 10을 초과하지 않으므로 술어함수를 만족하지 않는다. 따라서 두 번째 인자의 함수가 실행되지 않고 인자로 전달 받은 `'12345'`을 그대로 반환한다.
- `truncate('0123456789ABC')`는 문자열의 길이가 10을 초과하므로 술어함수를 만족한다. 따라서 `R.pipe(R.take(10), R.append('…'), R.join('')` 함수에 `'0123456789ABC'`값을 전달하여 실행을 한다. 최대 10개의 문자열을 앞에서 부터 취득해(take 함수는 기본적으로 배열의 원소를 취득하지만 문자열도 적용 가능) 배열로 반환 후, `R.append`으로 `'…'`를 배열에 추가하고 `R.join`으로 배열의 원소들을 문자열로 연결한 결과를 반환하므로 `'0123456789…'`가 된다.

## References
- https://ramdajs.com/docs/#when
