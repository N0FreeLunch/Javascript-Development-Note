## 프로미스

### 프로미스는 객체이다.
- 프로미스는 객체이다. `new Promise`로 프로미스 클래스로 프로미스 객체를 만들어 사용한다.
- 객체의 중요한 특징은 멤버 변수를 가지는 것으로 멤버 변수에 어떤 값이 들어가 있는지에 따라 다양한 객체의 상태를 만들 수 있다는 특징을 갖고 있다.
- 프로미스 객체는 세 가지의 상태 대기(pending), 이행(fulfilled), 거부(rejected) 중 하나의 상태를 갖는다.

### 프로미스의 목적

### 상태 변경의 방식
- 프로미스는 생성자로 함수를 받는다. 이 함수는 프로미스가 미래 어느 시점에 데이터를 취득했을 때, 데이터를 취득했어요. 데이터 취득을 실패했어요의 상태를 프로미스 객체에 기록하기 위한 것이다.
- 프로미스의 생성자 합수는 상태를 변경할 수 있는 `resolve`와 `reject`라는 함수를 받는다. `resolve` 함수를 실행하면 프로미스 인스턴스의 상태를 pending -> fulfilled 상태로 변경시키고, `reject` 함수를 실행하면 프로미스 인스턴스의 상태를 pending -> rejected 상태로 변경시킨다.
- 프로미스의 상태를 변경 시키기 위해서는 `resolve`나 `reject` 함수를 실행시켜야 하는데, 일반적으로 언제 실행될지 알 수 없는 비동기 동작이 이뤄졌을 때 비동기 동작의 결과에 따라 `resolve`나 `reject`를 실행시킴으로써 프로미스의 상태를 pending 상태에서 fulfilled나 rejected 상태로 변경시킨다.

### 예제코드
```js
let myFirstPromise = new Promise((resolve, reject) => {
  setTimeout(function () {
    resolve("성공!"); // 와! 문제 없음!
  }, 250);
});

myFirstPromise.then((successMessage) => {
  console.log("와! " + successMessage);
});
```
