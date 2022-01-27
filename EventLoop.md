## 이벤트 루프의 동작 위치
- 자바스크립트 엔진에서 동작하지 않는다.
- nodejs 또는 브라우저에서 이벤트 루프를 담당한다.

## 이벤트 루프의 큐
- 하나의 큐가 아닌 여러개의 큐가 복잡적으로 상호작용한다.

## 이벤트 루프의 스레드
- 단일 스레드에서 실행된다.

## 이벤트 루프의 큐에 위치한 작업
- FIFO(First In First Out) 방식으로 동작한다.
- 큐에 적재된 작업의 순서가 변경되는 일은 없다. FIFO에 의해서 먼저 들어간 작업이 먼저 처리된다.

## 이벤트 루프의 구조
```
Timer -> Pending i/o callbacks -> Idle, prepare -> Poll -> Check -> Close callbacks -> Timer
```
- 위 구조가 이벤트 루프이며 위 이벤트 루프와는 별도로 nextTickQueue와 mircroTaskQueue가 존재한다. (이 두개의 큐는 이벤트 루프의 일부가 아니다.)
- nextTickQueue와 mircroTaskQueue는 이벤트 루프의 각 페이즈(Timer, Pending i/o callbacks, Idle/prepare, Poll, Check, Close callbacks)와 별도로 작동한다. 별개의 작동을 하기 때문.

## 이벤트 루프의 페이즈
### Timer 페이즈
- 이벤트 루프의 시작을 알리는 페이즈








## Reference
- https://evan-moon.github.io/2019/08/01/nodejs-event-loop-workflow/
- http://voidcanvas.com/nodejs-event-loop/
- https://meetup.toast.com/posts/89
