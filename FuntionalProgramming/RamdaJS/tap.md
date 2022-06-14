
## 표현
```
(a → *) → a → a
```


## 예제
```
const sayX = x => console.log('x is ' + x);
R.tap(sayX, 100); //=> 100
// logs 'x is 100'
```
- `sayX`는 `x => console.log('x is ' + x)`
