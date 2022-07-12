## repeat
- R.repeat
> Returns a fixed list of size n containing a specified identical value.
- 정해진 특정한 값과 동일한 원소를 같는 크기가 n으로 정해진 리스트를 반환한다.
- 곧, 사이즈가 N인 배열을 반환하는데 배열의 모든 원소는 동일한 값을 가진다고 정의 할 수 있다.


## 표현
```
a → n → [a]
```
- 첫 번째 인자로 임의의 타입 a를 받는다.
- 두 번째 인자로 숫자를 받는다.
- 반환은 임의의 타임 a를 원소롤 하는 배열을 반환

## 설명
```
R.repeat(반복할 값, 반복할 횟수)
```
- 첫 번째 인자로 들어온 값을 두번째 인자로 들어온 수 만큼 반복하여 배열에 담아 반환한다.
- 값을 복사하므로 참조의 경우 주소만 복사하게 된다. 앝은 복사를 하는 것으로 반복된 참조 원소들을 `===`으로 비교했을 때 true를 반환한다.

## 예제
```
R.repeat('hi', 5); //=> ['hi', 'hi', 'hi', 'hi', 'hi']

const obj = {};
const repeatedObjs = R.repeat(obj, 5); //=> [{}, {}, {}, {}, {}]
repeatedObjs[0] === repeatedObjs[1]; //=> true
```
- `R.repeat('hi', 5);` `'hi'`라는 문자를 `5`번 반복하여 배열에 담아 반환
- `R.repeat(obj, 5);` 빈 오브젝트를 여러번 복사하여 배열에 담아 반환
- `repeat` 함수에 의해 복사된 값은 얕은 복사가 되기 때문에 같은 원본 오브젝트를 가리키게 됨(참조하는 원본 객체가 같다) 따라서 복사 된 두 오브젝트를 타입과 값이 일치하는지 여부를 확인하는 `===`를 사용했을 때 일치하여 `true`가 반환 된다. 

## Reference
- https://ramdajs.com/docs/#repeat
