## keysIn
> Returns a list containing the names of all the properties of the supplied object, including prototype properties. 
- 주어진 오브젝트의 프로토타입의 프로퍼티를 포함한 모든 프로퍼티 이름을 가진 리스트를 반환한다.

> Note that the order of the output array is not guaranteed to be consistent across different JS platforms.

## 표현
```
{k: v} → [k]
```
- `{k: v} →` 첫 번째 인자로 오브젝트를 받는다.
- `→ [k]` 오브젝트의 키(k)를 배열로 반환한다.

## 설명
- 하나의 오브젝트를 받아 받은 오브젝트의 프로퍼티 뿐만 아니라 프로토타입 체인으로 타고 올라가는 모든 프로퍼티를 반환한다.

## 예제
```
const F = function() { this.x = 'X'; };
F.prototype.y = 'Y';
const f = new F();
R.keysIn(f); //=> ['x', 'y']
```
- `F`라는 함수는 생성자로 `x`멤버 변수를 가지고 있다.
- F 함수의 프로토타입으로 y 프로퍼티를 설정한다.
-  F 함수를 클래스로 하여 인스턴스화한 객체 f의 프로퍼티들을 `keysIn`으로 확인하면 `['x', 'y']` 생성자로 만든 x 프로퍼티 뿐만 아니라 프로토타입의 y 프로퍼티도 반환한다.

## Reference
- https://ramdajs.com/docs/#keysIn
