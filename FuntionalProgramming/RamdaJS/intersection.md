## intersection
> Combines two lists into a set (i.e. no duplicates) composed of those elements common to both lists.
- 두 개의 리스트를 하나의 집합으로 합친다. (i.e. 복제를 하 않는다.) 양쪽 리스트의 공통 엘리먼트로 구성됩니다.

## 표현
```
[*] → [*] → [*]
```
- `[*] →` 임의의 원소로 구성된 리스트를 받는다.
- `→ [*] →` 임의의 원소로 구성된 리스트를 받는다.
- `→ [*]` 두 리스트에서 공통된 원소를 담은 배열을 반환한다.

## 설명
- 두 리스트의 공통 원소를 뽑아 배열로 반환한다.

## 예제
```
R.intersection([1,2,3,4], [7,6,5,4,3]); //=> [4, 3]
```
- 두 리스트의 원소 중 같은 원소는 `4`, `3`이므로 `[4, 3]`가 반환된다.

## Reference
- https://ramdajs.com/docs/#intersection
