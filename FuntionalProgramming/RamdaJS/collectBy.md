## collectBy
> Splits a list into sub-lists, based on the result of calling a key-returning function on each element, and grouping the results according to values returned.
- 리스트의 각각의 원소에 대해 지정한 키에 대한 반환값을 얻는 함수를 호출한 결과에 따라 하나의 리스트를 여러 서브리스트로 분리한다. 함수를 호출한 결과에 따라 그룹으로 나눈다. 

## 설명

## 표현
```
Idx a => (b → a) → [b] → [[b]]
Idx = String | Int | Symbol
```

## 예제
```
R.collectBy(R.prop('type'), [
  {type: 'breakfast', item: '☕️'},
  {type: 'lunch', item: '🌯'},
  {type: 'dinner', item: '🍝'},
  {type: 'breakfast', item: '🥐'},
  {type: 'lunch', item: '🍕'}
]);

// [ [ {type: 'breakfast', item: '☕️'},
//     {type: 'breakfast', item: '🥐'} ],
//   [ {type: 'lunch', item: '🌯'},
//     {type: 'lunch', item: '🍕'} ],
//   [ {type: 'dinner', item: '🍝'} ] ]
```

## Reference
- https://ramdajs.com/docs/#collectBy
