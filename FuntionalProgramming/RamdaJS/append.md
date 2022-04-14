## append
- R.append

## 설명
- 두 번째 인자로 배열로 받고 첫 번째 인자로 받은 값을 배열에 추가한 형태의 배열을 반환한다.
- 특정 인자를 추가하는 함수를 만들고 이 함수에 배열을 넣고 평가하면 배열에 지정한 인자가 원소로 추가된 형태의 배열을 뽑아낸다는 의미이다. 

## 표현
```
a → [a] → [a]
```
- `a →` 첫 번째 인자로는 a 타입의 인자를 넣는다.
- `→ [a] →` 두 번째 인자로는 a 타입을 원소로 하는 배열을 넣는다.
- `→ [a]` 평가 결과는 a 타입을 원소로 하는 배열을 반환한다.


## 예제
```
R.append('tests', ['write', 'more']); //=> ['write', 'more', 'tests']
R.append('tests', []); //=> ['tests']
R.append(['tests'], ['write', 'more']); //=> ['write', 'more', ['tests']]
```
- `['write', 'more']` 배열에 `'tests'`라는 원소를 추가하여 `['write', 'more', 'tests']`가 되었다.
- 나머지도 마찬가지 원리

## Reference
- https://ramdajs.com/docs/#append
