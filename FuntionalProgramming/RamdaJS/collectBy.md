## collectBy
> Splits a list into sub-lists, based on the result of calling a key-returning function on each element, and grouping the results according to values returned.
- 리스트의 각각의 원소에 대해 지정한 키에 대한 반환값을 얻는 함수를 호출한 결과에 따라 하나의 리스트를 여러 서브리스트로 분리한다. 함수를 호출한 결과를 기준으로 그룹으로 묶는다.

## 설명
- 함수와 배열을 받고 주어진 함수에 배열의 원소가 할당 된 결과가 일치하는 대상끼리 배열로 묶고 이를 원소로 하여 나열한 배열을 반환한다.

## 표현
```
Idx a => (b → a) → [b] → [[b]]
Idx = String | Int | Symbol
```
- `Idx = String | Int | Symbol`: `Idx`란 것은 오브젝트의 키값으로 사용될 수 있는 타입을 총칭한다.
- `Idx a =>` 오브젝트의 키 값으로 사용될 수 있는 타입인 `a`에 대해
- `(b → a) →` 첫 번째 인자는 두 번째 인자로 받는 배열의 원소의 유형에 해당하는 값을 받아서 오브젝트의 키 값으로 사용될 수 있는 타입인 `a` 유형을 반환하는 함수를 받는다.
- `→ [b] →` 두 번째 인자는 배열을 받고, 이 배열 안의 원소는 모두 첫 번째 인자로 받은 함수의 인자로 할당 가능한 값이어야 한다.
- `→ [[b]]` 두 번째 인자로 받은 배열의 각 원소를 첫 번째 인자로 받은 함수에 넣고 반환된 결과 값이 같은 대상끼리 하나의 배열로 묶어서 이 배열을 원소로 하는 리스트를 반환한다.

## 예제
```
R.collectBy(R.prop('type'), [
  {type: 'breakfast', item: '☕️'},
  {type: 'lunch', item: '🌯'},
  {type: 'dinner', item: '🍝'},
  {type: 'breakfast', item: '🥐'},
  {type: 'lunch', item: '🍕'}
]);
```
- `R.prop('type')`은 자바스크립트 오브젝트에서 `type`이란 키가 갖고 있는 값을 뽑는 역할을 한다.
- 두 번째 인자로 받은 배열의 각 원소를 첫 번째로 인자로 받은 함수에 넣고 평가한다. 그러면 각 원소에서 `type` 키가 갖고 있는 값이 반환된다.
- `R.prop('type')({type: 'breakfast', item: '☕️'})`의 결과는 `'breakfast'`이다.
- `R.prop('type')({type: 'lunch', item: '🌯'})`의 결과는 `'lunch'`이다. 
- `R.prop('type')({type: 'dinner', item: '🍝'})`의 결과는 `'dinner'`이다.
- `R.prop('type')({type: 'breakfast', item: '🥐'})`의 결과는 `'breakfast'`이다.
- `R.prop('type')({type: 'lunch', item: '🍕'})`의 결과는 `'lunch'`이다.
- 앞선 원소로 부터 `'breakfast'`, `'lunch'`, `'dinner'` 순으로 나왔고 각각에 대해 동일한 결과를 갖는 대상으로 묶는다.
- `'breakfast'`는 `{type: 'breakfast', item: '☕️'}`, `{type: 'breakfast', item: '🥐'}`을 묶는다.
- `'lunch'`는 `{type: 'lunch', item: '🌯'}`, `{type: 'lunch', item: '🍕'}`를 묶는다.
- `'dinner'`는 `{type: 'dinner', item: '🍝'}` 만 묶인다.
- 각각의 묶음을 배열로 묶고, 묶음을 배열의 원소로 나타낸 결과는 다음과 같다.
```
// [ [ {type: 'breakfast', item: '☕️'},
//     {type: 'breakfast', item: '🥐'} ],
//   [ {type: 'lunch', item: '🌯'},
//     {type: 'lunch', item: '🍕'} ],
//   [ {type: 'dinner', item: '🍝'} ] ]
```

## Reference
- https://ramdajs.com/docs/#collectBy
