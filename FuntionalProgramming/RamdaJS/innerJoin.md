## innerJoin
> Takes a predicate pred, a list xs, and a list ys, and returns a list xs' comprising each of the elements of xs which is equal to one or more elements of ys according to pred.

> pred must be a binary function expecting an element from each list.

> xs, ys, and xs' are treated as sets, semantically, so ordering should not be significant, but since xs' is ordered the implementation guarantees that its values are in the same order as they appear in xs. Duplicates are not removed, so xs' may contain duplicates if xs contains duplicates.


## 표현
```
((a, b) → Boolean) → [a] → [b] → [a]
```
- `((a, b) → Boolean)` 두 개의 인자를 받아 참 거짓을 판단하는 술어함수를 받는다.
- `→ [a] →` 첫 번째 인자로 배열을 받아 술어함수의 첫 번째 인자에 넣는다.
- `→ [b] →` 두 번째 인자로 배열을 받아 술어함수의 두 번째 인자에 넣는다.
- 두 번째로 받은 배열의 원소와 세 번째로 받은 배열의 원소의 카르테시안 곱에 해당하는 원소 쌍을 술어 함수의 인자로 넣어 참을 만족하는 대상을 두 번째 인자의 배열에서 뽑는다.

## 설명

## 예제
```
R.innerJoin(
  (record, id) => record.id === id,
  [{id: 824, name: 'Richie Furay'},
   {id: 956, name: 'Dewey Martin'},
   {id: 313, name: 'Bruce Palmer'},
   {id: 456, name: 'Stephen Stills'},
   {id: 177, name: 'Neil Young'}],
  [177, 456, 999]
);
//=> [{id: 456, name: 'Stephen Stills'}, {id: 177, name: 'Neil Young'}]
```
- `(record, id) => record.id === id` 첫 번째 인자로 오브젝트를 받아서 오브젝트의 id 프로퍼티 두 번째 인자로 id 값을 받아서 일치하는지 확인하는 함수이다.
- 두 번째 인자로 `[{id: 824, name: 'Richie Furay'}, ..., {id: 177, name: 'Neil Young'}]` 원소가 오브젝트인 배열을 받는다.
- 세 번째 인자로 `[177, 456, 999]` 원소가 수인 배열을 받는다.
- 술어 함수의 인자로 `({id: 824, name: 'Richie Furay'}, 177)`, `({id: 956, name: 'Dewey Martin'}, 177)`,  `({id: 313, name: 'Bruce Palmer'}, 177)`, ... , `({id: 313, name: 'Bruce Palmer'}, 999)`, `({id: 456, name: 'Stephen Stills'}, 456)`, `({id: 177, name: 'Neil Young'}, 999)`으로 두 번째 인자의 배열에서 5개 X 세 번째 인자의 배열에서 3개로 15가지 조합의 인자 구성을 술어 함수의 인자로 할당하고 술어함수를 참으로 만족하는 값을 뽑으면 `id: 456, name: 'Stephen Stills'}`, `{id: 177, name: 'Neil Young'}`이고 이를 배열로 반환하므로 `[{id: 456, name: 'Stephen Stills'}, {id: 177, name: 'Neil Young'}]`가 된다.

## Reference
- https://ramdajs.com/docs/#innerJoin
