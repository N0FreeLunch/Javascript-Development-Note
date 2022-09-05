## 생성자 정의
```
function Person(first, last, age, gender, interests) {
  this.name = {
    first,
    last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
};
```

## 메소드 정의
```
Person.prototype.greeting = function() {
  alert('Hi! I\'m ' + this.name.first + '.');
};
```

## 사람 클래스를 이용해서 Teacher 클래스 만들기
- 사람클래스와 Teacher 클래스는 상속 관계로 만들 수 있다.
- 사람 클래스의 하위 클래스로 Teacher 클래스를 만들고 사람클래스가 가진 멤버에 멤버를 추가하거나 멤버를 오버라이드 할 수 있다.
- 자바스크립트에는 기본적으로 상속 표현이 없다. ES6 이후로 클래스와 상속을 표현하는 문법이 추가 되었지만 기존의 자바스크립트 구현 방식을 활용한 것이다. ES6 이전의 자바스크립트에서 상속을 어떻게 표현했을까?
- 다른 객체를 정의할 때 상속할 객체가 가진 메소드를 가져오는 방식으로 만들며 이 때 사용하는 문법이 `call` 메소드이다.

```
function Teacher(first, last, age, gender, interests, subject) {
  Person.call(this, first, last, age, gender, interests);

  this.subject = subject;
}
```
- 객체의 `call` 메소드를 호출하면 객체가 가진 속성들이 현재의 컨텍스트에 바인딩 된다.
- `Person` 객체의 속성을 this에 call 한다는 의미로 해석하면 된다.
- `Person`이 가진 속성과 동일한 속성을 갖도록 어트리뷰트를 정해주면 된다.
- `this.subject = subject;` 이 코드는 Person 객체에는 없는 새로운 객체를 추가하였다.

```
function Teacher(first, last, age, gender, interests, subject) {
  this.name = {
    first,
    last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
  this.subject = subject;
}
```
- 객체지향에서 중요한 것은 상속을 받았다고 한다면 해당 객체의 조상이 누군지 확인할 수 있어야한다는 것인데 이렇게 정의를 하게 되면 공통 선조를 가진 클래스인지 알 수 없게 되는 문제가 생긴다. 또한 상속을 상위 객체를 변경했을 때 하위 객체의 변경이 일어나지 않는 문제점이 있다. 따라서 call 메소드를 사용해 컨텍스트의 객체에 바인딩을 하자.

## Reference
- https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Classes_in_JavaScript
