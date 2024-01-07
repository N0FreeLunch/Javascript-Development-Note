## nthArg
> Returns a function which returns its nth argument.

### 설명


### 표현
```
Number → *… → *
```

### 예제
```js
R.nthArg(1)('a', 'b', 'c'); //=> 'b'
R.nthArg(-1)('a', 'b', 'c'); //=> 'c'
```
- `R.nthArg(1)`는 1번 인덱스에 해당하는 인자를 반환하는 함수이다. 이 함수의 인자에 `('a', 'b', 'c')`가 들어가면 `'a'`는 0, `'b'`는 1, `'c'`는 2번 인덱스에 해당하므로 1번 인덱스에 해당하는 `'a'`가 결과값으로 반환된다.
- `R.nthArg(-1)`는 -1번 인덱스에 해당하는 인자를 반환하는 함수이다. 이 함수의 인자에 `('a', 'b', 'c')`가 들어가면 뒤에서 부터 `'c'`는 -1, `'b'`는 -2, `'a'`는 -3번 인덱스에 해당하므로 -1번 인덱스에 해당하는 `'c'`가 결과값으로 반환된다.

## Reference
- https://ramdajs.com/docs/#nthArg
