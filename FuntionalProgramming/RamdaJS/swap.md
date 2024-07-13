## swap
> Swap an item, at index indexA with another item, at index indexB, in an object or a list of elements. A new result will be created containing the new elements order.
- 오브젝트 또는 원소들의 리스트에서 첫번째 인자(indexA)와 다른 인자(indexB)의 값을 서로 교체한다. 새로운 원소와 순서를 포함한 결과를 생성한다.

### 설명
- 첫 번째 인자와 두 번째 인자로 지정한 인덱스, 프로퍼티의 값을 서로 교환한다. 값만 교환 되며, 키에 해당하는 인덱스나 프로퍼티는 그대로 유지된다.
- 배열, 오브젝트, 문자열을 대상으로 사용할 수 있으며 배열은 인덱스를 받고 

### 표현
```
Number → Number → [a] → [a]
```
- `Number →`: 첫 번째 인자로 교환할 대상 인덱스 번호를 받는다.
- `→ Number →`: 두 번째 인자로 첫 번째 인자로 선택된 값과 교환할 대상의 인덱스 번호를 받는다.
- `→ [a] →`: 세 번째 인자로 배열을 받는다.
- `→ [a]`: 첫 번째 인자와 두 번째 인자로 선택된 값을 서로 교체한 결과를 반환한다. 값만 교환하므로 구조는 서로 같다.

#### 추가
- 공식 문서에는 적혀있지 않지만 다음과 같은 표현이 가능하다.
```
Number → Number → String → String 
```
```
Idx → Idx → {k: v} → {k: v}
Idx = String | Int | Symbol
```

### 예제
```
R.swap(0, 2, ['a', 'b', 'c', 'd', 'e', 'f']); //=> ['c', 'b', 'a', 'd', 'e', 'f']
R.swap(-1, 0, ['a', 'b', 'c', 'd', 'e', 'f']); //=> ['f', 'b', 'c', 'd', 'e', 'a']
R.swap('a', 'b', {a: 1, b: 2}); //=> {a: 2, b: 1}
R.swap(0, 2, 'foo'); //=> 'oof'
```
- `R.swap(0, 2, ['a', 'b', 'c', 'd', 'e', 'f'])` 0번 인덱스인 'a'와 2번 인덱스인 'c'의 값을 서로 교환하므로 그 결과는 `['c', 'b', 'a', 'd', 'e', 'f']`가 된다.
- `R.swap(-1, 0, ['a', 'b', 'c', 'd', 'e', 'f'])` -1번 인덱스는 마지막 인덱스고 마지막 인덱스 값은 'f'이다. 이것과 0번 인덱스인 'a'의 값을 서로 교환하므로 그 결과는 `['f', 'b', 'c', 'd', 'e', 'a']`가 된다.
- `R.swap('a', 'b', {a: 1, b: 2}); //=> {a: 2, b: 1}` a 프로퍼티의 값인 1과 b 프로퍼티의 값인 2를 서로 교환한다. 그 결과는 `{a: 2, b: 1}`가 된다.
- `R.swap(0, 2, 'foo'); //=> 'oof'` 문자열의 0번 인덱스는 f이고, 2번 인덱스는 o이다. 서로 교환하면 `'oof'`가 된다.

## Reference
- https://ramdajs.com/docs/#swap
