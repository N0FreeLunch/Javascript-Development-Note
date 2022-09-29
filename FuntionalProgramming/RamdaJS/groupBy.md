## groupBy
> Splits a list into sub-lists stored in an object, based on the result of calling a key-returning function on each element, and grouping the results according to values returned.

> Dispatches to the groupBy method of the second argument, if present.

> Acts as a transducer if a transformer is given in list position.

## 표현
```
Idx a => (b → a) → [b] → {a: [b]}
Idx = String | Int | Symbol
```
- `Idx = String | Int | Symbol`의 종류는 문자열 또는 정수 또는 심볼 타입이다. 이렇게 지정한 이유는 최종적으로 오브젝트의 프로퍼티명으로 사용 가능한 것이 문자열, 정수, 심볼이기 때문이다.
- `Idx a  =>` 순서를 지정할 수 있는 종류를 `a`라고 하자.
- `(b → a) →` 첫 번째 인자로 함수를 하나 받는다. 함수는 하나의 인자를 받고 반환 값으로 `Idx`로 지정한 종류를 반환 되어야 한다.
- `→ [b] →` 두 번째 인자로 첫 번째 인자로 받은 함수의 인자로 할당할 수 있는 종류를 원소로 하는 배열을 받는다.
- `→ {a: [b]}` 첫 번째 인자에서 반환 된 값을 프로퍼티명으로 하고 두 번째 인자로 받은 배열의 원소가 첫 번째 함수를 통과하고 얻은 결과를 프로퍼티명으로 할 때 동일한 프로퍼티 명으로 분류된 원소로 해당 프로퍼티명의 벨류로 넣는 배열의 원소로 넣은 형태의 오브젝트를 얻는다.

## 설명
- 첫 번째 인자로 함수를 받는다. 함수는 하나의 인자를 받아서 해당 인자에 대한 그룹명을 반환하는 함수이다.
- 두 번째 인자로 배열을 받는다. 배열의 원소는 첫 번째 인자의 함수의 인자로 할당할 수 있어야 한다.
- `groupBy` 함수에 두 인자가 할당되면, 두 번째 인자의 배열을 순회하여 원소를 하나씩 첫 번째 인자로 넣어진 함수의 인자로 넣고 함수를 평가한다. 해당 평가 결과 값으로 두 번째 인자의 원소들을 그룹화 한다.
- 반환 값은 그룹명을 프로퍼티로 하고 그룹화된 원소를 담은 배열을 벨류로 하는 오브젝트가 반환 된다.

## 예제
```
const byGrade = R.groupBy(function(student) {
  const score = student.score;
  return score < 65 ? 'F' :
         score < 70 ? 'D' :
         score < 80 ? 'C' :
         score < 90 ? 'B' : 'A';
});
const students = [{name: 'Abby', score: 84},
                {name: 'Eddy', score: 58},
                // ...
                {name: 'Jack', score: 69}];
byGrade(students);
// {
//   'A': [{name: 'Dianne', score: 99}],
//   'B': [{name: 'Abby', score: 84}]
//   // ...,
//   'F': [{name: 'Eddy', score: 58}]
// }
```
- `student.score`는 student 오브젝트를 받아서 오브젝트의 score 프로퍼티를 확인한다.
- 65점 이하면 F를, 그 이상 70점 미만이면 D를, 그 이상 80점 미만이면 C를, 그 이상 90점 미만이면 B를, 그 이상 이면 A를 반환하는 함수이다.
- `R.groupBy` 함수로 첫 번째 인자로는 배열의 원소를 하나 할당하여 생성할 그룹명을 지정하고, 두 번째 인자로는 첫 번째 인자의 함수의 인자로 할당할 수 있는 원소로 구성된 배열을 받는다.
- `{name: 'Abby', score: 84}`를 받아서 84점이므로 B그룹에 넣고, `{name: 'Eddy', score: 58}`를 받아서 58점이므로 F그룹에 넣고, `{name: 'Jack', score: 69}`를 받아서 D그룹에 넣고, `{name: 'Dianne', score: 99}`를 받아서 A그룹에 넣는다.
- 오브젝트의 프로퍼티명으로 그룹명, 값으로 그룹에 해당하는 배열의 원소를 담은 배열을 할당한다.
- 따라서 결과는 다음과 같다.
```
{
  'A': [{name: 'Dianne', score: 99}],
  'B': [{name: 'Abby', score: 84}]
   ...,
  'F': [{name: 'Eddy', score: 58}]
}
```

## Reference
- https://ramdajs.com/docs/#groupBy
