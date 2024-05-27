## transduce
> Initializes a transducer using supplied iterator function. Returns a single item by iterating through the list, successively calling the transformed iterator function and passing it an accumulator value and the current value from the array, and then passing the result to the next call.
- 주어진 순회 함수를 사용하여 변환기(transducer)을 초기화 한다. 리스트를 순회하면서 연속적으로 변환된(transformed) 순회 함수를 호출하여 하나의 아이템을 반환한다. 호출하는 순회 함수에 누산기(accumulator) 값과 배열의 현재 값을 (인자로) 전달하며 (순회함수의) 다음 호출에 순회 함수의 결과 값을 전달한다.

> The iterator function receives two values: (acc, value). It will be wrapped as a transformer to initialize the transducer. A transformer can be passed directly in place of an iterator function. In both cases, iteration may be stopped early with the R.reduced function.
- 순회 함수는 두 값(acc, value)를 받는다. 변형기(transformer) 함수를 레핑하여 변환기(transducer)를 초기화 한다. 순회 함수 대신에 transformer를 전달 할 수 있다. 두 경우 모두 R.reduced 함수를 사용하여 조기 종료 할 수 있다.

> A transducer is a function that accepts a transformer and returns a transformer and can be composed directly.
- 변환기(transducer)는 transformer 함수를 받고, 변형기(transformer)를 반환하고 직접 합성할 수 있는 함수이다.

> A transformer is an object that provides a 2-arity reducing iterator function, step, 0-arity initial value function, init, and 1-arity result extraction function, result. The step function is used as the iterator function in reduce. The result function is used to convert the final accumulator into the return type and in most cases is R.identity. The init function can be used to provide an initial accumulator, but is ignored by transduce.
- transformer는 2개의 인자를 받는 축소 반복자 함수(reducing iterator function)인 step 함수, 그리고 0개의 인자를 받는 초기값 함수(initial value function), 1개의 인자를 받는 결과 추출 함수(result extraction function)인 result 함수를 제공하는 객체이다. 결과 추출 함수는 누적된 최종 값을 반환 타입으로 변환하는데 사용된다. 결과 추출함수는 대부분의 경우 (최종값을 변경하지 않고 그대로 반환하는) R.identity (항등함수)이다. 초기 함수는 초기 누산기(accumulator)(누적을 계산할 때 사용되는 초기값)를 제공하는데 사용될 수 있지만, transduce에서는 무시된다.

> The iteration is performed with R.reduce after initializing the transducer.
- 순회 작업은 변환기(transducer)를 초기화한 후 `R.reduce`를 사용하여 수행된다.

> See also reduce, reduced, into.

### 설명
- reduce 함수와 비슷한 동작을 한다. 하지만 첫 번째 인자로 최종 누산기 값을 reduce 함수의 평가값으로 반환할 때 변환을 담당하는 변환기(transducer) 함수를 추가로 받는다.
- 첫 번째 인자로는 변환기(transducer) 함수를 받고, 두 번째 인자로는 순회 함수를 받고, 세 번째 인자로는 누산기의 초기값을 받고, 네 번째 인자로 배열을 받는다.
- 배열의 각 원소를 하나씩 순회함수에 대입을 하며 순회 함수는 누산기 값과 순회 대상 원소를 받아 반환 값을 다음 순회 함수의 누산기 인자 값으로 전달한다.
- 배열의 최종 원소에 순회 함수를 적용하고 반환된 최종 누산값에 첫 번째 인자로 받은 변환기 함수에 전달하고 그 결과를 최종 평가 값으로 반환한다.

### 표현
```
(c → c) → ((a, b) → a) → a → [b] → a
```
- `(c → c) →`: 첫 번째 인자로 변환기(transducer) 함수를 받는다. 변환기는 누적된 최종 결과를 최종 반환 값으로 변환할 때 사용되는 함수이다.
- `→ ((a, b) → a) →`: 두 번째 인자로 순회 함수를 받는다. 순회 함수는 누적값(a)와 배열을 순회할 때의 적용 원소(b)를 전달 받아 다음 순회 함수에 전달할 누적값(a)를 반환한다.
- `→ a → `: 세 번째 인자는 초기 누산기 값(accumulator value)으로, 첫 번째 순회함수에 전달할 누적값이 존재하지 않으므로 이 때 전달하는 값이다.
- `→ [b] →`: 네 번째 인자는 순회할 대상 오브젝트를 의미한다.
- `→ a`: 누적된 최종 값을 반환한다.

### 예제
```js
const numbers = [1, 2, 3, 4];
const transducer = R.compose(R.map(R.add(1)), R.take(2));
R.transduce(transducer, R.flip(R.append), [], numbers); //=> [2, 3]

const isOdd = (x) => x % 2 !== 0;
const firstOddTransducer = R.compose(R.filter(isOdd), R.take(1));
R.transduce(firstOddTransducer, R.flip(R.append), [], R.range(0, 100)); //=> [1]
```

#### 첫 번째 예제
```js
R.transduce(transducer, R.flip(R.append), [], numbers);
```
- `R.map(R.add(1))`은 대상을 순회하면서 각각의 요소에 1을 더하는 함수로 인자로 대상을 받는다. `R.take(2)`는 배열의 첫 번째 요소부터 지정한 갯수의 요소를 나열한 배열을 반환한다. `R.compose`은 오른쪽 함수의 평가 결과를 왼쪽 함수로 전달하여 합성하는 함수이다. 따라서 `transducer`는 배열을 인자로 받아서 배열의 원소를 첫 번째 원소 부터 연속된 2개의 요소만 추출한 배열의 원소 각각에 1을 더하기 위한 함수이다.
- `R.append`는 배열의 끝에 인자를 하나 추가하는 함수로 `R.flip`은 함수의 첫 번째 인자와 두 번째 인자의 순서를 바꾼 함수를 만든다. 따라서 `R.flip(R.append)`은 베열을 첫 번째 인자로 받고 두 번째 인자로 추가할 값을 받는 함수가 된다. 이 함수는 순회 함수가 위치하는 파라메터에 할당되었다. 순회 함수는 첫 번째 인자로 누산기(accumulator)를 받고, 두 번째 인자로 순회하는 요소의 값을 받는다. 순회 함수가 되어야 했기 때문에 `R.append`를 그대로 사용하는 것이 아닌 첫 번째와 두 번째 인자의 순서를 바꾸는 `R.flip` 함수에 전달을 했다.
- 순회 함수는 반환 값으로 배열에 원소를 추가하는 작업을 하므로 누산기(accumulator)의 초기값으로는 빈 배열을 사용한다.
- `[1, 2, 3, 4]`에 대해 첫 번째 순회에서는 누산기 `[]`과 현재 원소 `1`을 전달 받아 `[1]`을 반환한다. 두 번째 순회에서는 `[1]`과 현재 원소 `2`을 전달 받아 `[1, 2]`를 반환한다. 이렇게 최종 순회를 거쳐 누산기 값은 `[1, 2, 3, 4]`이며 여기서 `transducer`을 적용하여 첫 번째 원소에서 2개의 원소를 추출한 배열 `[1, 2]`의 원소 각각에 1을 더해 `[2, 3]`을 반환한다.
- 최종 누산기 값에 적용되는 `transducer` 함수를 적용하기 전의 과정은 배열을 순회하여 새로운 각 원소에 함수를 적용한 반환 값을 갖는 배열을 받는 것으로 map 함수와 같은 역할을 하는 기능을 사용하였다. map 함수는 기존 배열을 통해 새로운 배열을 만들어내는데 이는 빈 배열에 각 순회 함수의 결과를 적용하여 map 함수를 만들 수 있다는 것을 보여준다.

#### 두 번째 예제
```js
R.transduce(firstOddTransducer, R.flip(R.append), [], R.range(0, 100));
```
- `isOdd`는 인자로 넣은 값이 홀수인지 확인하는 술어 함수이다. `R.compose(R.filter(isOdd), R.take(1))`는 배열에서 첫 번째 원소만을 꺼낸 배열의 원소의 값이 짝수이면 빈 배열을, 홀수이면 첫 번째 원소만을 꺼낸 배열 그대로를 반환한다. 따라서 변수의 이름도 `firstOddTransducer`으로 최종 누산기값의 첫 번째 원소가 홀수를 의미하는 변수명을 붙여 주었다.
- `R.range(0, 100)` 0부터 100까지의 정수가 차례로 든 배열을 리스트를 순회의 대상으로 한다.
- `[0, 1, 2, 3, ..., 99, 100]`에서 `R.flip(R.append)`에 첫 번째 순회에서는 초기값 `[]`과 `0`을 전달하면, `[0]`이 반환된다. 두 번째 순회에서는 첫 번째 순회의 결과값 `[0]`과 현재 요소 `[1]`을 전달하여 `[0, 1]`이 된다. 세 번째 순회에서는 두 번째 순회의 결과값 `[0, 1]`과 현재 요소 `[2]`를 전달하면 `[1, 2, 3]`이 된다. 이렇게 `[1, 2, 3, ... ,99 , 100]`가 된다. 0에서 2번 인덱스까지 추출하면 `[1, 2, 3]` 이런식으로 최종 누산기 값은 `[1, 2, 3, ... , 99, 100]`가 된다. 여기서 첫 번째 원소만을 추출한 배열은 `[1]`이며, 원소의 값이 홀수이므로 `[1]` 그대로 반환한다.

## Reference
- https://ramdajs.com/docs/#transduce
