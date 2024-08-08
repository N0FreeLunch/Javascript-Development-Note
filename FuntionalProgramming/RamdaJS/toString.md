## toString
> Returns the string representation of the given value.
- 주어진 값의 문자열 표현을 반환한다.
> eval'ing the output should result in a value equivalent to the input value.
- 출력을 평가하면(eval'ing) 입력 값과 동일한 값을 생성해야 한다.
> Many of the built-in toString methods do not satisfy this requirement.
- 많은 내장된 toString 메소드는 이러한 요구사항을 만족하지 못한다.

> If the given value is an [object Object] with a toString method other than Object.prototype.toString, this method is invoked with no arguments to produce the return value.
- 만약 주어진 값이 (오브젝트가 문자열로 표기 되었을 때의 디폴트 값인) `[object Object]`이고 (표기 형태는 같고) Object.prototype.toString 이외의 toString 매소드를 가졌다면, 이 메소드는 인수 없이 호출되어 반환 값을 생성한다.
> This means user-defined constructor functions can provide a suitable toString method. For example:
- 이것은 사용자 정의 생성자 함수가 적합한 toString 메소드를 제공한다는 것을 의미한다. 예를 들어 (예제 참고)

### 설명
- 주어진 값의 문자열 값을 호출한다. 문자열 값을 판단하기 위해서 각 객체의 `.prototype.toString`의 값을 호출한 결과를 사용한다.
- 자바스크립트의 기본 타입은 해당 타입의 여러 유틸리티를 가진 오브젝트로 변환이 될 수 있고, 모든 객체는 `Object.prototype.toString` 값을 갖고 있으며 내장 객체의 종류에 따라 `.prototype.toString`가 해당 객체의 종류에 맞게 정의되어 있으므로 문자열로 변환되는 대상에 따라 문자열의 표기 방식이 달라질 수 있다. 만약 특별한 `.prototype.toString`가 없다면 `Object.prototype.toString`가 호출되고 이는 `[object Object]`으로 표기된다.

### 표현
```
* → String
```
- `* →`: 첫 번째 인자로 임의의 값을 받는다. 이 값은 값의 문자열 표기 방식을 반환할 대상이다.
- `→ String`: 반환된 결과는 첫 번째 인자 값의 문자열 표기값을 반환한다.

### 예제
```js
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function() {
  return 'new Point(' + this.x + ', ' + this.y + ')';
};

R.toString(new Point(1, 2)); //=> 'new Point(1, 2)'
```
- `Point`는 new 키워드롤 객채를 만들었을 때 x 프로퍼티와 y 프로퍼티를 갖는다. 각각의 값은 new으로 객체를 만들 때의 생성자에 전달한 값으로 만들어진다.
- `Point.prototype.toString`으로 오브젝트의 프로토타입에 정의된 디폴트 `toString` 메소드는 덮어씌워지며, 객체가 문자열로 호출되었을 때 `[object Object]`의 값이 되지만, 프로토타입의 toString 메소드가 덮어씌워져 있기 때문에 사용자 정의된 함수가 문자열으로 표현될 때 호출된다.
- `R.toString(new Point(1, 2))`는 `new Point(1, 2)`의 값이 문자열 표현의 값이 반환되는데, 유저 정의된 `Point.prototype.toString`에 정의된 함수가 호출된 결과값을 반환한다. 따라서 그 결과는 `'new Point(1, 2)'`가 된다.

```js
R.toString(42); //=> '42'
R.toString('abc'); //=> '"abc"'
R.toString([1, 2, 3]); //=> '[1, 2, 3]'
R.toString({foo: 1, bar: 2, baz: 3}); //=> '{"bar": 2, "baz": 3, "foo": 1}'
R.toString(new Date('2001-02-03T04:05:06Z')); //=> 'new Date("2001-02-03T04:05:06.000Z")'
```
- 자바스크립트의 원시 타입에 .을 붙여 프로퍼티를 접근하게 되면 원시 타입에 대응하는 객체로 자동 형변환이 된다. 자동 형변환이 되면 각 타입의 기본 객체의 `.prototype.toString`을 호출하여 문자열로 변환된 값을 얻는다.
- `R.toString(42)`: 수 `42`의 문자열 표현은 `'42'`이다.
- `R.toString('abc')`: 문자열 `'abc'`의 문자열 표현은 `"abc"`이다.
- `R.toString([1, 2, 3])`: 배열 `[1, 2, 3]`의 문자열 표현은 `"[1, 2, 3]"`이다.
- `R.toString({foo: 1, bar: 2, baz: 3})`: 오브젝트 `{foo: 1, bar: 2, baz: 3}`의 문자열 표현은 `'{"bar": 2, "baz": 3, "foo": 1}'`이 된다.
- `R.toString(new Date('2001-02-03T04:05:06Z'))`: 내장 날짜 객체의 문자열 표현은 `'new Date("2001-02-03T04:05:06.000Z")'`가 된다.

## References
- https://ramdajs.com/docs/#toString
