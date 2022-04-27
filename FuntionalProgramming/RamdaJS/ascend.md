## ascend
- R.ascend

## 설명
- 

## 표현
```
Ord b => (a → b) → a → a → Number
```

## 예제
```
const byAge = R.ascend(R.prop('age'));
const people = [
  { name: 'Emma', age: 70 },
  { name: 'Peter', age: 78 },
  { name: 'Mikhail', age: 62 },
];
const peopleByYoungestFirst = R.sort(byAge, people);
  //=> [{ name: 'Mikhail', age: 62 },{ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 }]
```

## Reference
- https://ramdajs.com/docs/#ascend
