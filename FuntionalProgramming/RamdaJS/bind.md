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

## Reference
- https://ramdajs.com/docs/#bind
