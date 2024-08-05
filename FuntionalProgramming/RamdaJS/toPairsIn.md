## toPairsInv
> Converts an object into an array of key, value arrays.
- 오브젝트를 키, 벨류의 배열들로 이뤄진 배열으로 변환한다.

> The object's own properties and prototype properties are used.
- 대상 오브젝트는 프로퍼티를 가지거나 프로토타입(prototype) 프로퍼티가 사용되어야 한다.

> Note that the order of the output array is not guaranteed to be consistent across different JS platforms.
- 다양한 자바스크립트 플렛폼(각 브라우저의 자바스크립트 파싱 엔진)에서 출력되는 배열의 순서는 일관성이 보장되지 않는다.

### 설명
- toPairs와 마찬가지로 오브젝트의 키-밸류 쌍을 [키, 벨류] 형태를 원소로 하는 배열로 변환한다. 그러나 toPairs가 프로토타입 프로퍼티를 변환 대상으로 하지 않는 것과 달리 오브젝트의 프로토타입 프로퍼티도 변환한다.

### 표현
```
{String: *} → [[String,*]]
```
- `{String: *} →`: 첫 번째 인자로 오브젝트를 받는다. 이 때 문자열 프로퍼티가 존재한다면 대응되는 값과 함께 [키, 벨류] 형태로 전환된다.
- `→ [[String,*]]`: 첫 번째 인자의 오브젝트의 프로퍼티와 프로토타입 프로터티를 [문자열의 키, 벨류] 형태의 배열로 변환하고 이들을 나열한 배열을 반환한다.

### 예제
```js
const F = function() { this.x = 'X'; };
F.prototype.y = 'Y';
const f = new F();
R.toPairsIn(f); //=> [['x','X'], ['y','Y']]
```
- 자바스크립트에서 new 키워드로 객체를 찍어낼 수 있는 클래스를 만들 수 있는데, 이 클래스는 class 문법이 도입되기 전에는 function 키워드를 사용한 함수로 만들었다.
- `function() { this.x = 'X'; }`는 new 키워드로 이 함수를 선언하면 객체가 하나 만들어지는데 이 객체는 `x`라는 프로퍼티를 가지며, 해당 프로퍼티의 값은 `'X'`라는 의미를 가진다.
- 그리고 자바스크립트에서 정적 멤버 역할을 하는 대상은 자바스크립트의 클래스의 prototype으로 연결된 오브젝트에 만들 수 있는데 이는 function 키워드로 오브젝트가 생성될 때 함께 생성되는 원본의 역할을 하는 오브젝트이다.
- function 키워드로 만들어진 모든 함수는 사본으로 시작하며, 원본인 prototype을 가지고 있다. new 키워드로 새로운 객체를 생성할 때는 사본의 데이터가 변경이 되더라도 원본의 데이터의 변경이 없다면 원본의 정보를 주형으로 새로운 사본이 생겨난다.
- 원본의 정보를 직접 변경하기 위해서 `prototype.y`를 사용하여 원본의 y값을 `'Y'`으로 정의하였다.
- `new F()`으로 새로운 사본을 생성할 때 생성된 오브젝트의 x 프로퍼티는 `'X'` 값을 가지고, 이어진 원본의 y 프로퍼티는 `'Y'` 값을 가지고 있다. `R.toPairsIn`은 사본의 프로퍼티와 원본의 프로퍼티 모두를 변환하므로 `[['x','X'], ['y','Y']]`의 결과값을 갖는다.

## Reference
- https://ramdajs.com/docs/#toPairsIn
