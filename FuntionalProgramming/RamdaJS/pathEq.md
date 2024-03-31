## pathEq
> Determines whether a nested path on an object has a specific value, in R.equals terms. Most likely used to filter a list.
- 오브젝트가 가진 특정한 값이 오브젝트 내부의 특정한 경로의 값인지 아닌지 판단한다. 일치 여부를 판단할 때는 R.equals의 룰을 따른다. 대개 리스트를 필터하는 용도로 사용된다.

> See also whereEq, propEq, pathSatisfies, equals.

### 설명
- 특정한 값이 오브젝트의 내부의 경로에서 지정한 값과 일치하는지를 확인하는 함수이다.
- 첫 번째 인자로 일치하는지 확인하려는 값을 받는다.
- 두 번째 인자로 배열에 원소를 나열한 경로를 지정한다. 배열에 나열된 순서대로 오브젝트의 키나 배열의 인덱스에 접근하면서 값을 탐색한다.
- 세 번째 인자로 탐색할 대상 오브젝트를 넣어준다.

### 표현
```
a → [Idx] → {a} → Boolean
Idx = String | Int | Symbol
```
- `Idx = String | Int | Symbol`: Idx는 오브젝트 내부의 경로를 탐색하기 위한 것으로 오브젝트의 키로 가능한 타입을 넣어 나열된 순서대로 오브젝트 내부의 값을 접근하는 용도로 사용한다.
- `a →`: 첫 번째 인자로 오브젝트 내에서 일치하는지 확인하기위한 값을 할당한다.
- `→ [Idx] →`: 두 번째 인자로 오브젝트 내부에서 탐색할 대상 경로를 지정한다. 
- `→ {a} →`: 탐색할 대상 오브젝트로 오브젝트 내부에는 탐색할 값인 `a`가 존재한다.
- `→ Boolean`: 오브젝트 내부의 주어진 경로의 값이, 첫 번째 인자의 값과 일치하면 true, 아니면 false를 반환한다.

### 예제
```js
const user1 = { address: { zipCode: 90210 } };
const user2 = { address: { zipCode: 55555 } };
const user3 = { name: 'Bob' };
const users = [ user1, user2, user3 ];
const isFamous = R.pathEq(90210, ['address', 'zipCode']);
R.filter(isFamous, users); //=> [ user1 ]
```
- `R.pathEq(90210, ['address', 'zipCode'])`: `pathEq`는 일치하는지 확인할 값, 경로, 대상 오브젝트를 받아야 하는데 2개의 인자만을 받는다. 커링에 의해 인자를 하나 더 받아 평가되는 함수인 `isFamous`를 반환한다.
- `R.filter(isFamous, users);`, `isFamous`는 오브젝트를 하나 더 받아 참, 거짓을 반환하는 술어함수이므로 필터 함수와 함께 쓰여 오브젝트를 원소로 하는 리스트에 대해 술어함수를 만족하는 원소를 찾아낸다.

## Reference
- https://ramdajs.com/docs/#pathEq
