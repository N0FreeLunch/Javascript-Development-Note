## aperture

> Returns a new list, composed of n-tuples of consecutive elements. If n is greater than the length of the list, an empty list is returned.
- 연속된 원소들의 n-튜플의 (원소로) 구성된 새로운 리스트를 반환한다. 만약 n(값)이 리스트의 길이(값)보다 크다면 빈 리스트가 반환된다.

> Acts as a transducer if a transformer is given in list position.
- 만약 변형기(transformer)가 리스트 위치에 주어졌다면 변환기(transducer)으로 작용한다.

> See also [transduce](./transduce.md).

### 설명

- 지정한 원소의 수를 n 이라고 할 때, 첫 번째 인덱스에서 순차적으로 n개의 원소를 뽑고, 두 번째 인덱스에서 뒤따르는 원소를 순차적으로 n개를 뽑는 방식으로, 세 번째 인덱스에서도 마찬가지로 계속해서 n개의 원소를 뽑아 n개의 원소를 뽑을 수 있는 인덱스의 원소까지 진행하여 n개씩 뽑은 원소를 하나의 배열로 하여 이 배열을 나열한 집합을 반환한다.
- `[a,b,c,d,e,f]`라고 하면 2개씩 뽑으면 `[[a,b], [b,c], [c,d], [e,f]]`가 되고, 3개씩 뽑으면 `[[a,b,c], [b,c,d], [c,d,e], [d,e,f]]`가 되는 식이다.
- 여기서 사용된 튜플은 연속된 요소들을 묶은 그룹이란 의미로 다른 프로그래밍 언어의 불변하는 배열의 의미하는 튜플과는 다른 개념이란 점에 주의하자. 이를 각각 Ramda의 튜플과 프로그래밍 언어의 튜플이라 하자. 프로그래밍 언어에서 튜플이란 데이터 구조는 배열처럼 원소를 나열한 것이지만 배열이 원소를 수정, 추가, 삭제 할 수 있는 반면, 튜플은 수정, 추가, 삭제를 할 수 없는 데이터 구조로 사용된다. 하지만 여기서 쓰인 튜플은 프로그래밍 언어의 튜플이 아닌, 연속된 원소 묶음을 의미하는 용어로 `[[a,b,c], [b,c,d], [c,d,e], [d,e,f]]`에서 튜플은 `[a,b,c]`, `[b,c,d]`, `[c,d,e]`, `[d,e,f]`에 해당한다. 하나의 배열이 길이 3의 튜플로 구성되어 있으므로 'n-tuples'라고 표현되어 있다. 프로그래밍 언어의 불변의 튜플이란 의미로 쓰였다면 `Object.freeze()`로 Ramda의 각 튜플을 변경할 수 없도록 고정시켜서 `Object.isFrozen()` 메소드로 판별 했을 때 true으로 판단되는 동결된 배열이어야 튜플이라고 부를 수 있을 것이지만, 변경할 수 있는 배열이기 때문에 프로그래밍 언어의 튜플은 아니다.

### 문법
```
R.aperture(n, list): Array
```
- `n`: The size of the tuples to create
- `list`: The list to split into n-length tuples
- Returns Array The resulting list of `n`-length tuples

### 표현

```
Number → [a] → [[a]]
```
- `Number →`: 첫 번째 인자로는 뽑아낼 원소의 갯수를 넣어야 하기 때문에 Number 타입을 받는다. 좀 더 엄밀하게는 자연수를 받을 수 있다.
- `→ [a] →`: 두 번째 인자로는 뽑아낼 대상을 배열으로 받는다. 이때 배열의 원소는 어떤 종류 a으로 동일한 종류여야 한다.
- `→ [[a]]`: 함수의 평가 값은 타입 a가 들어간 (첫 번째 인자로 받은 값의 길이 만큼의 원소를 가진) 배열(= 튜플)을 원소로 한 배열이 된다.

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
