## transduce
> Initializes a transducer using supplied iterator function. Returns a single item by iterating through the list, successively calling the transformed iterator function and passing it an accumulator value and the current value from the array, and then passing the result to the next call.
- 주어진 순회 함수를 사용하여 변환기(transducer)을 초기화 한다. 리스트를 순회하면서 연속적으로 변환된(transformed) 순회 함수를 호출하여 하나의 아이템을 반환한다. 호출하는 순회 함수에 누산기(accumulator) 값과 배열의 현재 값을 전달하며 (순회함수의) 다음 호출에 순회 함수의 결과 값을 전달한다.

> The iterator function receives two values: (acc, value). It will be wrapped as a transformer to initialize the transducer. A transformer can be passed directly in place of an iterator function. In both cases, iteration may be stopped early with the R.reduced function.
- 순회 함수는 두 값(acc, value)를 받는다. transformer 함수를 레핑하여 transducer를 초기화 한다. 순회 함수 대신에 transformer를 전달 할 수 있다. 두 경우 모두 R.reduced 함수를 사용하여 조기 종료 할 수 있다.

> A transducer is a function that accepts a transformer and returns a transformer and can be composed directly.
- 변환기(transducer)는 transformer를 받고, transformer를 반환하고 직접 합성할 수 있는 함수이다.

> A transformer is an object that provides a 2-arity reducing iterator function, step, 0-arity initial value function, init, and 1-arity result extraction function, result. The step function is used as the iterator function in reduce. The result function is used to convert the final accumulator into the return type and in most cases is R.identity. The init function can be used to provide an initial accumulator, but is ignored by transduce.
- transformer는 2개의 인자를 받는 축소 반복자 함수(reducing iterator function)인 step 함수, 그리고 0개의 인자를 받는 초기값 함수(initial value function), 1개의 인자를 받는 결과 추출 함수(result extraction function)인 result 함수를 제공하는 객체이다. 결과 추출 함수는 누적된 최종 값을 반환 타입으로 변환하는데 사용된다. 결과 추출함수는 대부분의 경우 (최종값을 변경하지 않고 그대로 반환하는) R.identity (항등함수)이다. 초기 함수는 초기 누산기(accumulator)(누적을 계산할 때 사용되는 초기값)를 제공하는데 사용될 수 있지만, transduce에서는 무시된다.

> The iteration is performed with R.reduce after initializing the transducer.
- 순회 작업은 변환기(transducer)를 초기화한 후 R.reduce를 사용하여 수행됩니다.

> See also reduce, reduced, into.

### 설명

### 표현
```
(c → c) → ((a, b) → a) → a → [b] → a
```

### 예제
```js
const numbers = [1, 2, 3, 4];
const transducer = R.compose(R.map(R.add(1)), R.take(2));
R.transduce(transducer, R.flip(R.append), [], numbers); //=> [2, 3]

const isOdd = (x) => x % 2 !== 0;
const firstOddTransducer = R.compose(R.filter(isOdd), R.take(1));
R.transduce(firstOddTransducer, R.flip(R.append), [], R.range(0, 100)); //=> [1]
```

## Reference
- https://ramdajs.com/docs/#transduce
