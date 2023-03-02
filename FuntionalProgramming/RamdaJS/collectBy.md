## collectBy
> Splits a list into sub-lists, based on the result of calling a key-returning function on each element, and grouping the results according to values returned.

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
