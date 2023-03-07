## comparator
> Makes a comparator function out of a function that reports whether the first element is less than the second.
- 비교하는 함수를 하나 만든다. 이 함수는 첫 번째 원소가 두 번째 원소보다 작은지를 보고하는 함수이다.

## 설명

## 표현
```
((a, b) → Boolean) → ((a, b) → Number)
```

## 예제
```
const byAge = R.comparator((a, b) => a.age < b.age);
const people = [
  { name: 'Emma', age: 70 },
  { name: 'Peter', age: 78 },
  { name: 'Mikhail', age: 62 },
];
const peopleByIncreasingAge = R.sort(byAge, people);
  //=> [{ name: 'Mikhail', age: 62 },{ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 }]
```
- `sort` 함수는 비교 함수에 인자를 번갈아 넣어본다. 비교함수가 불리언값을 반환하는 경우에는 두 인자의 일치 여부를 확인하기 위해서는 두 인자를 번갈아 넣어야 알 수 있기 때문이다. 오브젝트와 오브젝트의 순서를 정하기 위해 비교 함수를 사용한 것이므로 비교함수에 따라 오브젝트의 순서를 결정하는 논리가 수치 비교가 아닐 경우도 존재한다. 수치인 경우에는 `a - b`가 음수인지 0인지 양수인지에 따라서 대소관계를 알 수 있지만, 비교가 수치로 판단하지 못하고 비교함수를 통해서 알 수 있고 비교함수가 불리언으로 값을 반환할 경우에는 두 오브젝트가 순서상 서로 같은지를 알기 위해서는 비교함수에 인자를 번갈아 넣어서 순서의 우위 관계를 정할 수 없는 상황을 만들어야 한다.
- `byAge({ name: 'Peter', age: 78 }, { name: 'Emma', age: 70 })`의 결과는 `false`이다. `false`는 `0`에 해당하므로 첫 번째 인자는 두 번째 인자보다 크다.
- `byAge({ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 })`의 결과는 `true`이다. `true`는 `1`에 해당하므로 첫 번째 인자는 두 번째 인자보다 작다.
- 따라서 결과는 `{ name: 'Emma', age: 70 }`, `{ name: 'Peter', age: 78 }` 순이된다. 이제 여기서 큰 것(`{ name: 'Peter', age: 78 }`)과 다음 원소(`{"name": "Mikhail", "age": 62}`)를 비교하자.
- `byAge({"name": "Mikhail", "age": 62}, {"name": "Peter", "age": 78})`의 결과는 `true`이다. `true`는 `1`에 해당하므로 첫 번째 인자는 두 번째 인자보타 작다.

## Reference
- https://ramdajs.com/docs/#comparator
