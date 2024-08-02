## takeWhile
> Returns a new list containing the first n elements of a given list, passing each value to the supplied predicate function, and terminating when the predicate function returns false.
- 주어진 리스트의 처음의 n개의 원소들을 포함하는 새로운 리스트를 반환한다. 주어진 술엄함수에는 (리스트) 각각의 원소 값을 전달하며, 술어함수가 false를 반환하면 (순회가) 종료된다.
> Excludes the element that caused the predicate function to fail.
- (순회가 종료되기 전에 마지막으로 false가 반환되는) 술어 함수를 실패로 만드는 원소는 배제한다.
> The predicate function is passed one argument: (value).
- 술어함수는 하나의 인자(value)를 받는다.

> Dispatches to the takeWhile method of the second argument, if present.
- 만약 두 번째 인자에 takeWhile 메소드가 존재한다면 takeWhile 메소드를 실행한다.

> Acts as a transducer if a transformer is given in list position.
- 만약 리스트를 받는 위치에 transformer가 주어지면, 변환기(transducer)로 행동한다.

> See also dropWhile, transduce, addIndex.

### 설명
- 주어진 원소의 집합(문자열, 배열)에서 원소의 나열된 순서상 첫 번째 인자부터 차례로 술어함수를 통과 시키고 술어함수가 연속으로 true를 만족하는 원소들만 모은 집합을 반환한다.

### 표현

#### 배열의 경우
```
(a → Boolean) → [a] → [a]
```

#### 문자열의 경우
```
(a → Boolean) → String → String
```

### 예제
```js
const isNotFour = x => x !== 4;

R.takeWhile(isNotFour, [1, 2, 3, 4, 3, 2, 1]); //=> [1, 2, 3]

R.takeWhile(x => x !== 'd' , 'Ramda'); //=> 'Ram'
```
- `isNotFour`는 4의 값을 인자로 받으면 false를 반환하는 술어 함수이다.
- `R.takeWhile(isNotFour, [1, 2, 3, 4, 3, 2, 1])`: 주어진 배열의 첫 번째 원소 부터 차례로 술어함수에 전달하면 그 반환 값은 '인자: 반환값'으로 표기할 때 1: true, 2: true, 3: true, 4: false가 된다. 따라서 4의 값에서 순회는 종료하게 되고 false를 반환한 4의 값은 제외하고 나머지 원소를 동일한 순으로 나열한 배열 `[1, 2, 3]`을 반환한다.
- `R.takeWhile(x => x !== 'd' , 'Ramda')`: 술어 함수는 'd'라는 문자가 나오면 false 그렇지 않으면 true를 반환하는 술어함수를 받고, 주어진 문자열에 대해 첫 번째 문자부터 술어함수의 인자로 전달하면 '인자: 반환값'으로 표기할 때 R: true, a: true, m: true, d: false가 된다. 따라서 d 값에서 순회는 종료하게 되고 false를 반환한 d를 제외한 나머지 문자를 동일한 순으로 나열한 문자 `'Ram'`을 반환한다.

## Reference
- https://ramdajs.com/docs/#takeWhile
