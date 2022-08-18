## 자바스크립트에서 객체
- 자바스크립트에서는 대부분이 객체이다.

## 빈 객체 만들기
```
var person = {};
```

### 브라우저에서 빈 객체의 표기
```
[object Object]
Object { }
{ }
```

## 멤버가 정의된 객체
```
const person = {
  name: ['Bob', 'Smith'],
  age: 32,
  gender: 'male',
  interests: ['music', 'skiing'],
  bio: function() {
    alert(this.name[0] + ' ' + this.name[1] + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  },
  greeting: function() {
    alert('Hi! I\'m ' + this.name[0] + '.');
  }
};
```
- 멤버 변수 : name, age, gender, interests
- 멤버 메소드 : bio, greeting

### 자바스크립트에서의 객체에서 멤버
- 자바스크립트 객체에는 키와 벨류를 설정할 수 있고, 키에 할당하는 값에 따라 멤버 변수도 되고 멤버 메소드로도 표현된다. 객체지향 언어와 달리 멤버변수와 멤버 메소드의 문법적인 구분이 없다.


## 객체 리터럴 (object literal)
- 멤버 변수에 해당하는 값을 프로퍼티(속성)으로 부르며, 멤버 메소드에 해당하는 값을 메소드라고 부른다.

## 네임스페이스
- 네임스페이스는 하나의 객체 내에서 다른 객체를 호출할 수 있도록 호출 객체를 지정할 수 있는 기능을 제공한다.

### 하위 네임스페이스
- 객체 내에 객체에 접근해야 할 때 내부의 객체에 접근하도록 지정하는 것을 하위 네임스페이스라고 한다.
```js
person = {
  name : {
    first: 'Bob',
    last: 'Smith'
  }
}
```

### 네임스페이스로 접근
```
person.name.first
person.name.last
```
- 객체의 멤버에 접근하는 방식이다.
- dot(.) 표기로 접근한다.

### 연관배열(associative arrays)로 접근
```
person['age']
person['name']['first']
```
- 배열은 원소에 접근하기 위한 방식으로 인덱스를 사용하여 접근하게 한다.
- 연관배열은 원소에 접근하기 위한 방식으로 인덱스 대신 원소의 이름으로 접근하게 한다.
- 자바스크립트의 객체는 배열은 아니지만 연관배열 방식으로 접근을 할 수 있다.

## 객체 접근 방식으로 객체의 멤버를 설정
```
person.age = 45;
person['name']['last'] = 'Cratchit';
```
```
person['eyes'] = 'hazel';
person.farewell = function() { alert("Bye everybody!"); }
```
- 위의 코드를 실행하면 객체 내부에 새로운 멤버가 생긴다.


## Reference
- [https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Basics)
