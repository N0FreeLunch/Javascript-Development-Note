## groupBy

> Splits a list into sub-lists stored in an object, based on the result of calling a key-returning function on each element, and grouping the results according to values returned.

> Dispatches to the groupBy method of the second argument, if present.

> Acts as a transducer if a transformer is given in list position.

## 설명

- 동일한 데이터 포멧의 데이터를 나열한 배열을 받아서, 해당 데이터를 콜백함수의 반환 값이 같은 것끼리 묶어 콜백 함수의 반환 값을 키로, 묶음 배열을 값으로 하는 오브젝트를 생성한다.
- 첫 번째 인자로 콜백 함수 하나를 받는다. 이 함수는 순회할 배열의 원소 하나를 인자로 전달 받고, 분류할 그룹명을 반환하는 함수이다. 반환되는 그룹명이 동일한 배열의 원소는 같은 그룹으로 묶이게 된다.
- 두 번째 인자로 배열을 받는다. 그룹화 할 데이터 리스트를 받는 것으로 배열의 원소를 그룹화 하기 위해서 배열의 원소는 첫 번째 인자 함수의 인자로 전달하여 그룹명을 반환 할 수 있는 값이어야 한다.
- `groupBy` 함수에 두 인자가 할당되면, 두 번째 인자의 배열을 순회하여 원소를 하나씩 첫 번째 인자로 전달하여 함수를 평가한다. 해당 평가 결과 값으로 두 번째 인자의 배열의 원소들을 그룹화 한다.
- 반환 값은 그룹명을 프로퍼티로 하고 그룹화된 원소를 담은 배열을 벨류로 하는 오브젝트가 반환 된다.

## 문법

```
R.groupBy(fn, list): Object
```
> `fn`: Function :: a -> Idx
- `fn`: (이 함수는 인자를 하나 받아서 오브젝트의 인덱스를 반환하는 함수이다.)
> `list`: The array to group
- `list`: 그룹화 할 배열
> Returns Object An object with the output of `fn` for keys, mapped to arrays of elements that produced that key when passed to `fn`.
- 오브젝트를 반환한다. 

## 표현

```
Idx a => (b → a) → [b] → {a: [b]}
Idx = String | Int | Symbol
```
- `Idx = String | Int | Symbol`: `Idx`의 종류는 문자열 또는 정수 또는 심볼 타입이다. 이렇게 지정한 이유는 최종적으로 오브젝트의 프로퍼티명으로 사용 가능한 것이 문자열, 정수, 심볼이기 때문이다.
- `Idx a  =>`: 순서를 지정할 수 있는 종류를 `a`라고 하자.
- `(b → a) →`: 첫 번째 인자로 함수를 하나 받는다. 함수는 하나의 인자를 받고 반환 값으로 `Idx`로 지정한 종류를 반환 되어야 한다.
- `→ [b] →`: 두 번째 인자로 첫 번째 인자로 받은 함수의 인자로 할당할 수 있는 종류를 원소로 하는 배열을 받는다.
- `→ {a: [b]}`: 첫 번째 인자에서 반환 된 값을 프로퍼티명으로 하고 두 번째 인자로 받은 배열의 원소가 첫 번째 함수를 통과하고 얻은 결과를 프로퍼티명으로 할 때 동일한 프로퍼티 명으로 분류된 원소로 해당 프로퍼티명의 벨류로 넣는 배열의 원소로 넣은 형태의 오브젝트를 얻는다.

## 예제

```js
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
- 따라서 결과는 다음과 같다.4

```js
{
  'A': [{name: 'Dianne', score: 99}],
  'B': [{name: 'Abby', score: 84}]
   ...,
  'F': [{name: 'Eddy', score: 58}]
}
```

## References

- https://ramdajs.com/docs/#groupBy
- https://github.com/ramda/ramda/blob/master/test/groupBy.js
- https://github.com/ramda/types/blob/develop/types/groupBy.d.ts
