## comparator

> Makes a comparator function out of a function that reports whether the first element is less than the second.
- 비교하는 함수를 하나 만든다. 이 함수는 첫 번째 원소가 두 번째 원소보다 작은지를 보고하는 함수이다.

## 설명

- 대상의 순서를 결정하기 위해서 첫 번째 인자가 두 번째 인자보다 작은지 판단하는 술어함수를 받아 정렬함수 등에서 순서 결정함수로 쓰는 함수를 생성한다.
- 정렬 함수 `sort` 등에서 받은 리스트의 원소 순서를 결정하기 위한 순서 결정함수가 `comparator` 함수이다. 리스트에서 두 원소씩 순서 결정 함수에 넣고 원소간의 순서를 결정한다.
- `comparator` 함수는 하나의 술어 함수를 인자로 받아 비교 함수를 만든다. 이 때 인자로 받는 술어함수는 순서를 비교하고 싶은 두 대상을 받아 참 거짓을 반환하는 함수이다.
- 인자로 받는 술어함수는 첫 번째 원소가 두 번째 원소보다 작으면 참을 반환하고 그렇지 않으면 거짓을 반환하는 함수이다. 인자의 할당 순서대로 작은 값과 큰 값이라고 보면 된다.
- `comparator` 함수에 술어함수를 넣어 평가되어 반환 된 함수는 `pred(a, b) ? -1 : pred(b, a) ? 1 : 0`의 로직을 갖는다.
- 반환된 함수의 '첫 번째 인자(`a`)가 두 번째 인자(`b`)보다 작으면'(= `pred(a, b)`) 술어함수(`pred`)는 `true`이므로 -1을 반환한다. '첫 번째 인자(`a`)가 두 번째 인자(`b`)보다 크면'(= `pred(b, a)`) `false`이므로 1을 반환한다. 인자가 두 번째 인자보다 작지도 크지도 않으면 0을 반환한다.
- 첫 번째 인자가 두 번째 인자보다 작은지를 판단하는 술어함수만으로도 순서 결정함수는 주어진 두 인자를 `a, b` 순서와 `b, a` 순으로 술어함수에 대입하여 두 인자의 순서가 누가 더 크고 작은지 같은지를 확인할 수 있다.
- 정렬 함수에서 일반적으로 기본적인 `comparator`으로 두 인자의 뺄셈을 통해서 순서를 비교한다. `comparator`는 첫 번째 원소가 두 번째 원소 보다 작은지를 확인하므로 두 번째 인자에서 첫 번째 인자를 빼는 방식을 사용한다. `b - a > 0`이면 결과값 `1`에 대응하며 `b > a`이며, `b - a < 0`이면 결과값 `-1`에 대응하며 `b < a`이며,  `b - a = 0`이면 결과값 `0`에 대응하며 `b = a`에 해당한다. 이를 통해 반환된 수(`-1`, `0` , `1`)를 통해서 두 인자의 순서가 정해진다.

## 문법

```
R.comparator(pred): Function
```

> pred : A predicate function of arity two which will return true if the first argument is less than the second, false otherwise
- pred : 두 인자를 받아 만약 첫 번째 인자가 두 번째 인자보다 작으면 true, 아니면 false를 반환하는 술어함수
> Returns function A Function :: a -> b -> Int that returns `-1` if a < b, `1` if b < a, otherwise `0`
- a -> b -> int으로 첫 번째 인자로 a를 받고, 두 번째 인자로 b를 받아서 a < b 일 때 -1, b < a 일 때 1, 나머지는 0인 세 정수를 반환하는 함수를 반환한다.

## 표현

```
((a, b) → Boolean) → ((a, b) → Number)
```

- `((a, b) → Boolean)`: 첫 번째 인자로 술어함수를 받는다. 이 술어함수는 두 인자를 받아서 순서를 결정하는 로직을 만들고 첫 번째 인자보다 두 번째 인자가 작다면 `true`, 아니면 `false`를 반환하는 함수이다.
- `→ ((a, b) → Number)`: `comparator` 함수는 인자를 하나 받고 함수를 평가를 하며 두 인자를 받아서 `-1`, `0`, `1`을 반환하는 함수를 생성한다.

## 예제

```js
const byAge = R.comparator((a, b) => a.age < b.age);
const people = [
  { name: 'Emma', age: 70 },
  { name: 'Peter', age: 78 },
  { name: 'Mikhail', age: 62 },
];
const peopleByIncreasingAge = R.sort(byAge, people);
  //=> [{ name: 'Mikhail', age: 62 }, { name: 'Emma', age: 70 }, { name: 'Peter', age: 78 }]
```

- `sort` 함수는 비교 함수에 인자를 번갈아 넣어본다. 비교함수가 불리언값을 반환하는 경우에는 두 인자의 일치 여부를 확인하기 위해서는 두 인자를 번갈아 넣어야 두 인자의 대소관계를 알 수 있기 때문이다.
- 위 예제는 오브젝트와 오브젝트의 순서를 정하기 위해 비교 함수를 사용한 것이므로 비교함수에 따라 오브젝트의 순서를 결정하는 논리가 수치 비교가 아닐 경우도 존재한다. 수치인 경우에는 `a - b`가 음수인지 0인지 양수인지에 따라서 대소관계를 알 수 있지만, 비교가 수치로 판단하지 못하고 비교함수를 통해서 알 수 있고 비교함수가 불리언으로 값을 반환할 경우에는 두 오브젝트가 순서상 서로 같은지를 알기 위해서는 비교함수에 인자를 번갈아 넣어서 순서의 우위 관계를 정할 수 없는 상황을 만들어야 한다.
- 정렬함수로 전달된 순서 비교함수는 인자를 번갈아 넣어가며 참 거짓의 판단 여부를 확인한다. 술어함수의 참 거짓에 따라 `pred(a, b) ? -1 : pred(b, a) ? 1 : 0` 로직에 따라 숫자가 반환된다.
- `byAge({ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 })`는 `pred(a, b)`에 해당하는 `((a, b) => a.age < b.age)({ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 })`는 `true`를 반환하므로 `-1`을 반환한다. 따라서 두 대상의 순서를 바꾸지 않는다.
- `byAge({ name: 'Peter', age: 78 }, { name: 'Mikhail', age: 62 })`는 `pred(a, b)`에 해당하는 `((a, b) => a.age < b.age)({ name: 'Peter', age: 78 }, { name: 'Mikhail', age: 62 })`는 `false`를 반환하므로 ` pred(b, a)`에 해당하는 `((a, b) => a.age < b.age)({ name: 'Mikhail', age: 62 }, { name: 'Peter', age: 78 })`를 실행하며 `true`이므로 1을 반환한다. 따라서 둘의 순서는 바뀐다.
- 브라우저에 따라 `sort` 함수의 정렬 알고리즘이 다르다. ECMA 표준에 특정 정렬함수를 지정하고 있지 않기 때문이다. 위에서는 원소를 순차적으로 넣은 방식으로 설명했지만 알고리즘에 따라 다른 방식으로 비교를 수행하게 된다. `sort`함수의 내부 동작에 따라 `byAge`함수에 전달되는 인자가 달라질 수 있지만 `sort`는 내부적으로 두 대상의 크기 비교를 하게 되어 있고 크기 비교를 통해서 전체 리스트의 원소들을 크기대로 정렬할 수 있다.

## References
- https://ramdajs.com/docs/#comparator
- https://github.com/ramda/ramda/blob/master/test/comparator.js
- https://github.com/ramda/types/blob/develop/types/compose.d.ts
