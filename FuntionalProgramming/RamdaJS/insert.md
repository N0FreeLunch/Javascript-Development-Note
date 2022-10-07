## insert
> Inserts the supplied element into the list, at the specified index. Note that this is not destructive: it returns a copy of the list with the changes.
> No lists have been harmed in the application of this function.

## 표현
```
Number → a → [a] → [a]
```
- `Number →` 두 번째 인자를 배열의 몇 번째 인데스에 넣을 것인지 정한다.
- `→ a →` 두 번째 인자로 배열에 집어 넣을 원소를 할당한다.
- `→ [a] →` 세 번째 인자로 대상 배열을 지정한다.
- `→ [a]` 주어진 배열의 지정한 인덱스에 주어진 원소를 넣고, 기존 인덱스의 원소 부터는 인덱스 번호가 +1이 된다.

## 설명
- 첫 번째 인자로 몇 번째 인덱스에 집어 넣을지를 지정한다.
- 두 번째 인자로 집어 넣을 대상을 설정한다.
- 세 번째 인자로 두 번째 인자로 받은 원소를 넣을 배열을 지정한다.
- 주어진 배열의 지정한 인덱스에 주어진 원소를 넣고, 넣어진 원소의 위치를 기준으로 기존 원소는 인덱스 번호가 +1이 된다.
- 연관 배열 형식이 아닌 수로 구성된 인덱스를 기준으로 한다.

## 예제
```
R.insert(2, 'x', [1,2,3,4]); //=> [1,2,'x',3,4]
```
- `[1,2,3,4]` 배열의 두 번째 인덱스에 `'x'`란 값을 집어 넣는다.
- 집어 넣은 인덱스 다음 부터는 기존 인덱스 번호 +1 이 되므로 `[1,2,'x',3,4]`가 된다.

## Reference
- https://ramdajs.com/docs/#insert
