## aperture

> Returns a new list, composed of n-tuples of consecutive elements. If n is greater than the length of the list, an empty list is returned.
- 연속된 원소들의 n-튜플의 구성인 새로운 리스트를 반환한다. 만약 n(값)이 리스트의 길이(값)보다 크다면 빈 리스트가 반환된다.

> Acts as a transducer if a transformer is given in list position.
- 만약 변형기(transformer)가 리스트 위치에 주어졌다면 변환기(transducer)으로 작용한다.

> See also [transduce](./transduce.md).

### 설명

- 지정한 원소의 수를 n 이라고 할 때, 첫 번째 인덱스에서 순차적으로 n개의 원소를 뽑고, 두 번째 인덱스에서 뒤따르는 원소를 순차적으로 n개를 뽑는 방식으로, 세 번째 인덱스에서도 마찬가지로 계속해서 n개의 원소를 뽑아 n개의 원소를 뽑을 수 있는 인덱스의 원소까지 진행하여 n개씩 뽑은 원소를 하나의 배열로 하여 이 배열을 나열한 집합을 반환한다.
- `[a,b,c,d,e,f]`라고 하면 2개씩 뽑으면 `[[a,b], [b,c], [c,d], [e,f]]`가 되고, 3개씩 뽑으면 `[[a,b,c], [b,c,d], [c,d,e], [d,e,f]]`가 되는 식이다.
- 배열이 원소를 순차적으로 나열한 것과 마찬가지로 튜플도 원소를 순차적으로 나열한 것이다. 배열이 원소를 수정, 추가, 삭제 할 수 있는 반면, 튜플은 수정, 추가, 삭제를 할 수 없는 개념이다. 자바스크립트의 배열은 불변하게 만들 수 없기 때문에 튜플이라고 부를 수 없지만, 함수형 언어의 용어를 차용해서 튜플으로 표현하기도한다.

### 표현
```
Number → [a] → [[a]]
```
- `Number →` 첫 번째 인자로는 뽑아낼 원소의 갯수를 넣어야 하기 때문에 Number 타입을 받는다.
- `→ [a]` 두 번째 인자로는 뽑아낼 대상을 Array 타입으로 받는다. 이때 원소는 어떤 타입 a이다.
- `→ [[a]]` 함수의 평가 값은  타입 a가 들어간 배열을 원소로 한 배열이 된다.

### 예제
```js
R.aperture(2, [1, 2, 3, 4, 5]); //=> [[1, 2], [2, 3], [3, 4], [4, 5]]
R.aperture(3, [1, 2, 3, 4, 5]); //=> [[1, 2, 3], [2, 3, 4], [3, 4, 5]]
R.aperture(7, [1, 2, 3, 4, 5]); //=> []
```
- `R.aperture(2, [1, 2, 3, 4, 5])` 첫 번째 인자로 뽑을 원소의 갯수 2를 지정한다. 두 번째 인자로 배열을 넣었다. 지정한 뽑을 원소 갯수 만큼 지정된 배열에서 첫번째 인덱스 부터 순차적으로 지정된 원소의 갯수만큼 뽑는다. `[1, 2, 3, 4, 5]` 첫번째 인덱스에서 2개를 뽑아 `[1, 2]` 두 번째 인덱스에서 2개를 뽑아 `[2, 3]` 세 번째 인덱스에서 2개를 뽑아 `[3, 4]` 네번째 인덱스에서 2개를 뽑아 `[4, 5]` 다섯번째 인덱스에서는 2개를 뽑을 수 없기 때문에 뽑지 않는다. 이 결과들을 배열안에 넣어 `[[1, 2], [2, 3], [3, 4], [4, 5]]`가 된다. 
- 나머지도 마찬가지 원리이므로 생략한다.

## References
- https://ramdajs.com/docs/#aperture
- https://github.com/ramda/ramda/blob/master/test/aperture.js
- https://github.com/ramda/types/blob/develop/types/aperture.d.ts
