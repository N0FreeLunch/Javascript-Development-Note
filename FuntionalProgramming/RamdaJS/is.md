## is
> See if an object (i.e. val) is an instance of the supplied constructor. This function will check up the inheritance chain, if any. If val was created using Object.create, R.is(Object, val) === true.
- 어떤 오브젝트가 주어진 생성자의 하나의 인스턴스인 경우, 이 함수가 체인되어 계승(inheritance) 된 함수인지 확인한다.
- 어떠한 경우에든 주어진 오브젝트(val)가 Object.create을 사용하여 만들어 졌다면 `R.is(Object, val) === true`이 된다.

## 표현
```
(* → {*}) → a → Boolean
```
- `(* → {*})` 첫 번째 인자로 인자를 하나 받아서 해당 해당 인자의 오브젝트 타입을 반환하는 함수를 넣는다. 프리미티브 타입의 값이라면 오브제트 타입의 값으로 강제 형변환을 한다.
- `→ a →` 두 번째 인자로 값을 받는다.
- `→ Boolean` 두 번째 인자가 첫 번째 인자를 체이닝한 값에 해당하면 참을 아니면 거짓을 반환한다.

## 설명
- 첫 번째 인자로 임의의 어떤 객체를 받는다.
- 두 번째 인자로 임의의 어떤 객체를 받는다.
- 두 번째 인자의 객체 첫 번째 인자로 받은 객체의 프로토타입 체인 된 객체인지 확인하고 참 거짓을 반환한다.
- `new 객체` 또는 `Object.create`등 기존 객체를 주형으로 하여 새로운 객체를 생성하는 방식으로 생성된 객체라면 `Object` 객체에서 체이닝 된 객체이므로 항상 `R.is(Object, 새로 생성된 객체)`가 참이 된다.

## 예제
```
R.is(Object, {}); //=> true
R.is(Number, 1); //=> true
R.is(Object, 1); //=> false
R.is(String, 's'); //=> true
R.is(String, new String('')); //=> true
R.is(Object, new String('')); //=> true
R.is(Object, 's'); //=> false
R.is(Number, {}); //=> false
```
- `R.is(Object, {})` 빈 오브젝트는 Object 객체를 체인하여 만들어지므로 참을 반환한다.
- `R.is(Number, 1)` 자바스크립트에서 수는 오브젝트이다. 1은 Number 객체를 체인하여 만들어지므로 참을 반환한다.
- `R.is(Object, 1)` 1은 Number 객체를 체인하여 만들어졌지만 Object 객체를 체인하여 만들어진 것은 아니다. 따라서 거짓을 반환한다.
- `R.is(String, 's')` 문자열은 String 객체를 체인하여 만들어지므로 참을 반환한다.
- `R.is(String, new String(''))` 문자열을 객체 생성 문법을 통해 만든 방식도 String 객체를 체인하여 만들어지므로 참을 반환한다.
- `R.is(Object, new String(''))` 문자열을 객체 생성 문법을 통해 만든 방식은 항상 참이므로 참을 반환한다.
- `R.is(Object, 's')` 문자열은 String 객체를 체인하여 만들어졌지만 Object 객체를 체인하여 만들어진 것은 아니다. 따라서 거짓을 반환한다.
- `R.is(Number, {})` 빈 오브젝트는 Object 객체를 체인하여 만들어졌지만 Number 객체를 체인하여 만들지 않으므로 거짓을 반환한다.

## Reference
- https://ramdajs.com/docs/#is
