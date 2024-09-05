## valuesIn
> Returns a list of all the properties, including prototype properties, of the supplied object.
- 주어진 오브젝트에서 모든 프로퍼티의 리스트를 반환한다. 프로토타입의 프로퍼티도 포함한다.
> Note that the order of the output array is not guaranteed to be consistent across different JS platforms.
- 출력된 배열의 순서는 JS 플렛폼(브라우저 엔진, NodeJS, Bun, Deno 등)이 달라질 때 보장되지 않는다.

> See also values, keysIn.

### 설명
- 주어진 오브젝트에서 모든 프로퍼티의 값만 추출해서 배열에 담은 결과를 얻는다.
- values가 프로토타입의 프로퍼티를 대상으로 하지 않는 것과 달리 valuesIn은 프로토타입의 프로퍼티가 가진 값도 포함한 배열을 반환한다.

### 표현
```
{k: v} → [v]
```
- `{k: v} →`: 첫 번째 인자로 오브젝트를 받는다.
- `→ [v]`:  오브젝트에서 키 정보는 제외하고 키의 값만을 프로토타입의 값을 포함하여 나열한 배열을 얻는다. 따라서 오브젝트의 벨류가 가진 종류 v를 배열의 원소 종류로 한다.

### 예제
```js
const F = function() { this.x = 'X'; };
F.prototype.y = 'Y';
const f = new F();
R.valuesIn(f); //=> ['X', 'Y']
```
- new 키워드를 통해서 새로운 객체를 생성하기 위해서는 자바스크립트의 클래스를 만들어야 하는데, 클래스 문법을 사용할 수도 있고, function 키워드를 통해서 클래스의 역할을 하는 오브젝트를 만들 수 있다. function 블록 안의 'this.멤버'로 new로 생성되는 객체의 멤버를 정의할 수 있고, 프로토타입을 사용하는 것을 통해서 다른 언어의 클래스의 정적 멤버와 유사한 정의를 할 수 있다.
- F 클래스를 주형으로 하여 f라는 인스턴스를 생성하였다. 인스턴스 멤버와 정적 멤버(프로토타입 멤버)의 값 모두를 나열하므로 `R.valuesIn(f)`의 값은 `['X', 'Y']`가 된다.

## References
- https://ramdajs.com/docs/#valuesIn
