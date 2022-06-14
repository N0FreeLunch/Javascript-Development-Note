## bind
- R.bind()

## 표현
```
(* → *) → {*} → (* → *)
```

## 설명
-
-


## 예제
```
const log = R.bind(console.log, console);
R.pipe(R.assoc('a', 2), R.tap(log), R.assoc('a', 3))({a: 1}); //=> {a: 3}
// logs {a: 2}
```
- `R.bind`라는 함수에 로그를 찍는 `console.log`함수와 `console` 오브젝트를 넣어 만든 함수를 log 변수에 넣었다.
- 대상 오브젝트 `{a: 1}`에 `R.assoc('a', 2)` a 프로퍼티에 2를 할당하고
- `R.assoc('a', 3)` a 프로퍼티에 3을 할당한다.

## Reference
- https://ramdajs.com/docs/#bind
