## without
> Returns a new list without values in the first argument.
- 첫 번째 인자(로 받는 값) 안의 값들을 제외한 새로운 리스트를 반환한다.
> R.equals is used to determine equality.
- (제외할 값과) 일치하는 대상을 판단할 때는 R.equals(함수)가 사용된다.
> Acts as a transducer if a transformer is given in list position.
- 만약 리스트(를 받는) 위치에 변형기가 주어지는 경우, 변환기로서 동작한다.
> See also [transduce](./transduce.md), [difference](./difference.md), [remove](./remove.md).

### 설명
- 전체집합(U)과 어떤 집합(A) 하나를 받아 해당 집합의 여집합인 'U - A'를 반환한다.
- 제외할 대상이 나열된 배열과 제외 당할 대상이 나열된 배열을 받아 제외 당할 대상에서 제외할 대상의 원소와 일치하는 원소를 제거한 배열을 반환한다. 반환된 배열의 나열 순서는 제외 당할 배열의 나열 순서를 따른다.

### 표현
```
[a] → [a] → [a]
```
- `[a] →`: 첫 번째 인자로 제외할 값을 나열한 배열을 받는다.
- `→ [a] →`: 두 번째 인자로 제외 당할 원소를 나열한 배열을 받는다.
- `→ [a]`: 두 번째로 받은 배열에서 첫 번째로 받은 인자를 제외한 나머지 배열을 받는다.

### 예제
```js
R.without([1, 2], [1, 2, 1, 3, 4]); //=> [3, 4]
```
- `[1, 2, 1, 3, 4]`에서 원소 1, 2를 제외하면 `[3, 4]`만이 남는다. 이를 반환 결과로 한다.

## References
- https://ramdajs.com/docs/#without
