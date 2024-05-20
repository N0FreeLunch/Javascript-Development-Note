## reduceBy
> Groups the elements of the list according to the result of calling the String-returning function keyFn on each element and reduces the elements of each group to a single value via the reducer function valueFn.
- 각 요소에 대해 문자열 반환 함수 keyFn을 호출한 결과에 따라 목록의 요소를 그룹화하고 reducer 함수 valueFn을 통해 각 그룹의 요소를 단일 값으로 줄인다.

> The value function receives two values: (acc, value). It may use R.reduced to short circuit the iteration.
- 함수는 (acc, value)의 두 값을 받는다. `R.reduced`를 사용한 간략한 순회 회로를 구성할 수 있다.

> This function is basically a more general groupBy function.
- 이 함수는 기본적으로 좀 더 일반적인 groupBy 함수에 해당한다.

> Acts as a transducer if a transformer is given in list position.

> See also groupBy, reduce, reduced.

### 설명
- 대상 원소를 받아 그룹명을 반환하는 함수로 대상을 그룹화하고, 각각의 그룹화 된 대상에 대해 R.reduce 함수를 적용한 결과를 값으로 한 키-벨류 쌍을 가진 오브젝트를 반환한다.

### 표현
```
((a, b) → a) → a → (b → String) → [b] → {String: a}
```
- `((a, b) → a) →`: 첫 번째 인자로 순회 할수를 할당한다. 순회 함수는 누적값 a와 현대 대상 요소 b를 받아, 다음 순회 함수의 누적값으로 전달 할 수 있는 값 `a`를 반환한다.
- `→ a →`: 두 번째 인자로 누산을 적용할 초기값을 받는다. 분류된 결과 그룹 각각에 대해 대상 원소를 순회하며, 각각의 그룹에 대해 순회 함수가 처음 실행될 때 이전 순회 함수의 결과값이 존재하지 않으므로 순회 함수는 이 초기값을 인자로 전달 받는다.
- `→ (b → String) →`: 세 번째 인자로는 배열의 대상 원소를 전달 했을 때 분류될 그룹명을 지정하는 함수이다.
- `→ [b] →`: 네 번째 인자로 순회할 대상 배열을 전달받는다. 배열의 각 요소는 순회 함수의 두 번째 인자로 전달되므로 순회 함수의 두 번째 파라메터와 동일한 종류인 b가 된다.
- `→ {String: a}`: 세 번째 인자로 받은 함수에 의해 분류된 그룹명을 키로 하고, 순회 함수의 결과 값을 값으로 하는 키-벨류 쌍을 가진 오브젝트를 반환한다. 이 때 오브젝트를 반환하는 것은 오브젝트는 키 값이 반드시 하나여야 하므로 키 값으로 그룹화 할 때 해당 키 값이 단일한 대상이라는 것을 문법적으로 나타내는 역할을 하기 때문이다.

### 예제
```js
const groupNames = (acc, {name}) => acc.concat(name)
const toGrade = ({score}) =>
  score < 65 ? 'F' :
  score < 70 ? 'D' :
  score < 80 ? 'C' :
  score < 90 ? 'B' : 'A'

var students = [
  {name: 'Abby', score: 83},
  {name: 'Bart', score: 62},
  {name: 'Curt', score: 88},
  {name: 'Dora', score: 92},
]

reduceBy(groupNames, [], toGrade, students)
//=> {"A": ["Dora"], "B": ["Abby", "Curt"], "F": ["Bart"]}
```
- `(acc, {name}) => acc.concat(name)`는 순회 함수를 의미한다. `.concat` 메소드는 [배열](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) 또는 [문자열](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat)에 대해 추가 배열에 원소를 추가하거나 문자열에 문자열을 연결하는 역할을 한다.
- `toGrade` 대상 원소를 받아 분류할 그룹을 반혼하는 keyFn 함수이다.
- `students`의 원소를 순회하면서 `toGrade` 함수에 따라 그룹화 한다. `{name: 'Abby', score: 83}`의 등급은 B, `{name: 'Bart', score: 62}`의 등급은 F, `{name: 'Curt', score: 88}`의 등급은 B, `{name: 'Dora', score: 92}`의 등급은 A이다.
- 누적값의 초기값은 `[]`이다. 각각의 등급에 대해 순회 함수를 적용하면, A는 []에 `'Dora'`을 추가한 `['Dora']`, B는 []에 `'Abby'`를 추가한 `['Abby']`을 누적값으로 전달 받아 `'Curt'`를 추가한 `['Abby', 'Curt']`, F는 []에 `Bart`를 추가한 `['bart']`가 된다.

## Reference
- https://ramdajs.com/docs/#reduceBy
