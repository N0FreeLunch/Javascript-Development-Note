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

### 왜 프로미스를 사용하는가?
- 프로미스 객체의 상태가 결정되는 순간, `resolve`와 `reject` 함수를 실행할 때 인자로 값을 전달하면, 이 값을 프로미스 객체에 `.then(콜백함수)`을 사용해서 콜백함수의 인자로 `resolve`나 `reject`으로 전달한 값을 전달 받을 수 있다.
- `.then`에 세팅한 콜백함수가 실행되는 시점은 `resolve`와 `reject`가 실행되는 시점이다. 곧, 프로미스의 생성자에 비동기 작업의 코드와 함께 비동기 작업의 결과를 가져오는 코드가 실행될 때 `resolve`와 `reject` 함수를 실행하는 것이다.

#### 고전적인 자바스크립트 프로그래밍
- 서버와의 통신이나 이미지를 가져오는 것과 같은 I/O작업을 하면, 얼마의 시간이 흘러야 데이터를 받아오는지 알 수 없는 경우가 있다. 가장 기본적으로 생각해 볼 수 있는 것은, 이들 값을 받아 올 때 어떤 변수의 상태를 바꾸는 것이다. 그리고 일정한 주기로 해당 변수의 값이 바뀌었는지 확인하고, 값이 바뀌었으면 주기적으로 확인하는 코드의 종료와 동시에 필요한 코드를 실행시키는 상황을 생각해 볼 수 있다.
```js
let loadingFlag = false;
setTimeout(() => { 
  console.log("loaded");
  loadingFlag = true;
}, Math.random()*5*1000);

const runAfterLoading = () => {
  console.log('next execution');
};

const checkLoadingFlag = setInterval(() => {
  if(loadingFlag) {
    clearInterval(checkLoadingFlag);
    console.log("load checked");
    runAfterLoading();
  } else {
    console.log("checking...");
  }
}, 500);

```

- setTimeout : 위의 `loadingFlag`가 true가 되는 때를 확인을 하고 코드를 실행하는 방식이다. 위의 코드는 `setTimeout`의 첫 번째 인자로 넣은 익명함수가 실행될 때까지 0~5초가 걸리는 `Math.random()*5*1000`와 함께 사용하였다.
- setInterval : 데이터를 받았을 때 `loadingFlag`가 true가 되므로 0.5초 마다 데이터를 받은 플레그가 변경되었는지를 체크한다. 플레그가 변경되었다면 더 이상 주기적으로 확인하지 않아도 되므로 `clearInterval`을 해 준다. `if(loadingFlag)` 조건문으로 실행되는 코드에 데이터를 받았을 때 실행할 코드 `runAfterLoading` 함수를 넣어준다.
