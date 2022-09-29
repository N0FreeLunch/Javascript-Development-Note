## groupBy
> Splits a list into sub-lists stored in an object, based on the result of calling a key-returning function on each element, and grouping the results according to values returned.

> Dispatches to the groupBy method of the second argument, if present.

> Acts as a transducer if a transformer is given in list position.

## 표현
```
Idx a => (b → a) → [b] → {a: [b]}
Idx = String | Int | Symbol
```

## 설명
- 첫 번째 인자로 함수를 받는다. 함수는 하나의 인자를 받아서 해당 인자에 대한 그룹명을 반환하는 함수이다.
- 두 번째 인자로 배열을 받는다. 배열의 원소는 첫 번째 인자의 함수의 인자로 할당할 수 있어야 한다.

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
- 따라서 결과는
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
