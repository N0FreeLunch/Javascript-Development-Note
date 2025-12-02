# hasIn

> Returns whether or not an object or its prototype chain has a property with the specified name
- 오브젝트의 프로토타입 체인이 지정한 이름의 프로퍼티를 가지고 있는지 아닌지를 반환한다.

## 설명

- has가 오브젝트의 프로퍼티만의 존재 유무를 확인했다면, hasIn은 오브젝트의 프로토타입의 프로퍼티의 존재 유무도 확인할 수 있다.
- 첫 번째 인자로 프로퍼티명을 지정한다.
- 두 번째 인자로 오브젝트를 받는다.
- 오브젝트 또는 오브젝트의 프로토타입이 가진 프로퍼티 중에서 지정한 프로퍼티명이 존재하면 참을 아니면 거짓을 반환한다.

## 문법

```
R.hasIn(prop, obj): Boolean
```
> `prop`: The name of the property to check for.
- `prop`: 확인할 프로퍼티의 이름
> `obj`: The object to query.
- `obj`: 쿼리할 오브젝트
> Returns Boolean Whether the property exists.
- 불리언을 반환한다. 프로퍼티가 존재하는지 하지 않는지(에 대한 불리언)

## 표현

```
s → {s: x} → Boolean
```
- `s →`: 두 번째 오브젝트의 프로퍼티명으로 지정 가능한 종류의 값을 받는다.
- `→ {s: x} →`: 오브젝트를 받는다.
- `→ Boolean`: 오브젝트와 오브젝트의 프로토타입 체인이 갖는 프로퍼티 중에서 지정한 프로퍼티명이 존재하면 참을 아니면 거짓을 반환한다.

## 예제

```js
function Rectangle(width, height) {
  this.width = width;
  this.height = height;
}
Rectangle.prototype.area = function() {
  return this.width * this.height;
};

const square = new Rectangle(2, 2);
R.hasIn('width', square);  //=> true
R.hasIn('area', square);  //=> true
```
- `Rectangle`은 함수이다. 자바스크립트에서 함수는 오브젝트이다. 자바스크립트는 함수를 실행할 때 전달 받은 인자의 값으로 오브젝트 내부의 초기값을 설정한다. `new` 키워드를 통해서 함수를 실행시킬 때 프로토 타입 객체를 주형으로 한 새로운 객체를 생성한다.
- `Rectangle.prototype.area`는 해당 오브젝트의 프로토타입에 프로퍼티를 설정한다. `Rectangle` 함수를 그냥 실행하든, `new` 키워드를 실행하든 프로토타입으로 설정한 키워드를 가지고 있다. 또한 자바스크립트의 클래스와 객체는 하나의 프로토타입 객체를 공유하고 있기 때문에 클래스의 스테틱 멤버와 동일한 역할을 한다.
- `new Rectangle(2, 2)` 새로운 객체를 만들어 냈을 때 프로토타입에 공유되는 객체가 존재하므로 `R.hasIn`을 사용하면 프로토타입에 존재하는 프로퍼티도 체크한다.
- `R.hasIn('width', square)`는 `square` 객체 내에 `'width'`라는 프로퍼티가 존재하므로 참을 반환한다.
- `R.hasIn('area', square)`는 `square` 객체의 프로토타입 내에 `'area'`라는 프로퍼티가 존재하므로 참을 반환한다.

## References

- https://ramdajs.com/docs/#hasIn
- https://github.com/ramda/ramda/blob/master/test/hasIn.js
- https://github.com/ramda/types/blob/develop/types/hasIn.d.ts

