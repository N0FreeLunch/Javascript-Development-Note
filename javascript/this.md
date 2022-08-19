## this
- 클래스 내의 코드에서 인스턴스화 된 객체를 가리킬 때 this 키워드를 사용한다.
- this는 실행 중인 코드가 속해있는 객체를 가리킨다.

```
var person1 = {
  name: 'Chris',
  greeting: function() {
    alert('Hi! I\'m ' + this.name + '.');
  }
}

var person2 = {
  name: 'Deepti',
  greeting: function() {
    alert('Hi! I\'m ' + this.name + '.');
  }
}
```
- 출력 결과는 "Hi! I'm Chris.", "Hi! I'm Deepti."이다.
