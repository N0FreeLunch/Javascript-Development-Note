## R.countBy
> Counts the elements of a list according to how many match each value of a key generated by the supplied function. 
> Returns an object mapping the keys produced by fn to the number of occurrences in the list.
> Note that all keys are coerced to strings because of how JavaScript objects work.
> Acts as a transducer if a transformer is given in list position.

## 표현
```
(a → String) → [a] → {*}
```
- `(a → String) →` 임의의 함수를 받는다. 결과 값이 문자열이 아니라면 문자열로 자동으로 형 변환된 값으로 계산한다.
- ` → [a] →` 값 배열을 받는다. 배열의 각 원소는 첫 번째 인자의 함수의 인자로 할당되어야 하기 때문에 동일 타입을 갖는다.
- `→ {*}` 배열에서 원소가 함수를 통과한 값과 일치되는 대상만을 뽑아 함수를 통과하기 전의 원소를 키로, 통과한 수의 값을 벨류로 하는 오브젝트를 반환한다.

## 설명
- `count`가 단순히 술어함수를 만족하는 대상의 갯수를 반환하는 함수인 것에 반해 `countBy`는 대상의 값이 술어 함수를 통과한 값과 일치하는 대상을 뽑아내는 것에 사용한다.
- 주어진 배열의 원소가 주어진 함수의 인자로 들어가 평가되었을 때의 결과와 동일한 값일 때의 대상을 뽑아 원소를 문자열화 한 것을 키로 함수를 통과한 결과 값을 벨류로 하는 오브젝트를 반환한다.

## 예제
```
const numbers = [1.0, 1.1, 1.2, 2.0, 3.0, 2.2];
R.countBy(Math.floor)(numbers);    //=> {'1': 3, '2': 2, '3': 1}

const letters = ['a', 'b', 'A', 'a', 'B', 'c'];
R.countBy(R.toLower)(letters);   //=> {'a': 3, 'b': 2, 'c': 1}
```
- `[1.0, 1.1, 1.2, 2.0, 3.0, 2.2]`에서 각각의 원소에 대해 `Math.floor`한 결과는 `1`, `1`, `1`, `2`, `3`, `2`이다. 함수를 통과한 값과 일치하는 대상은 `1.0`, `2.0`, `3.0`이다.
- 리스트의 1.0은 1의 결과를 가지며, 리스트의 2.0은 2의 결과를 가지며, 리스트의 3.0은 3의 결과를 갖는다. 이를 오브젝트 형식으로 변환하면 수 타입을 문자로 변환하는 기능 `Number.prototype.toString()`등의 자바스크립트 내장 형변환 기능에 의해서 `1.0`은 `'1'`로 `2.0`은 `2`로 `3.0`은 `3`으로 변환된다. 따라서 결과는 `{'1': 3, '2': 2, '3': 1}`이다.
- `['a', 'b', 'A', 'a', 'B', 'c']`에서 각각의 원소에 대해 `R.toLower`한 결관는 `a`, `b`, `a`, `a`, `b`, `c`이다. 함수를 통과한 값과 일치하는 대상은 `'a'`, `'b'`, `'a'`, `'c'`이다. 이를 오브제트로 변환하면 중복되는 키는 제거되므로 결과는 `{'a': 3, 'b': 2, 'c': 1}`이다.

## Reference
- https://ramdajs.com/docs/#countBy
