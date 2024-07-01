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

#### 배열인 경우
- `[a] →`: 첫 번째 인자로 배열을 받는다. 이 때 배열의 원소는 두 번째 인자로 받을 배열의 원소와 동일한 종류여야 한다.
- `→ [a] →`: 두 번째 인자로 배열을 받는다. 마찬가지로 첫 번째 배열의 원소와 동일한 종류의 원소를 가지는 배열이어야 한다.
- `→ Boolean`: 두 번째 인자로 받은 배열의 원소가 나열되는 시작점이 첫 번째 인자로 받은 배열에 나열된 원소와 순서와 값이 일치하는지 판단한 결과를 반환한다.

#### 문자열인 경우
- `String →`: 첫 번째 인자로 문자열을 받는다.
- `→ String →`: 두 번째 인자로 문자열을 받는다.
- `→ Boolean`: 두 번째 인자로 받은 문자열의 문자가 나열되는 시작점이 첫 번째 인자로 받은 문자열에 나열된 문자와 순서와 값이 일치하는지 판단한 결과를 반환한다.

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
