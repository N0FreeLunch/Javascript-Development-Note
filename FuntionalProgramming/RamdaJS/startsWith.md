## startsWith
> Checks if a list starts with the provided sublist.
- 리스트가 주어진 서브 리스트로 시작되는지 확인한다.

> Similarly, checks if a string starts with the provided substring.
- 문자열에 대해서도 비슷하게 동작하는데, 주어진 문자열이 주어진 부분 문자열로 시작하는지 확인한다.

> See also endsWith.

### 설명
- 주어진 리스트(배열이나 문자열)가 서브 리스트의 원소가 나열된 순으로 시작되고 있는지 확인하는 술어함수이다.

### 표현
```
[a] → [a] → Boolean
String → String → Boolean
```

### 예제
```js
R.startsWith('a', 'abc')                //=> true
R.startsWith('b', 'abc')                //=> false
R.startsWith(['a'], ['a', 'b', 'c'])    //=> true
R.startsWith(['b'], ['a', 'b', 'c'])    //=> false
```
- `R.startsWith('a', 'abc')`: 'abc'는 'a' 문자열로 시작되므로 참이다.
- `R.startsWith('b', 'abc')`: 'abc'는 'b' 문자열로 시작하지 않으므로 거짓이다.
- `R.startsWith(['a'], ['a', 'b', 'c'])`: `['a', 'b', 'c']`는 `['a']` 배열의 원소로 시작하므로 참이다.
- `R.startsWith(['b'], ['a', 'b', 'c'])`: `['a', 'b', 'c']`는 `['b']` 배열의 원소로 시작하지 않으므로 거짓이다.

## Reference
- https://ramdajs.com/docs/#startsWith
