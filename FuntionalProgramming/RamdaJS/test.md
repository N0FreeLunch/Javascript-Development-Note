## test
> Determines whether a given string matches a given regular expression.
- 주어진 정규 표현식에 주어진 문자열이 매칭되는지(정규식을 통과하는 대상이 있는지)를 확인한다.

> See also match.

### 설명

### 표현
```
RegExp → String → Boolean
```
- `RegExp →`: 첫 번째 인자로 정규 표현식을 받는다.
- `→ String →`: 두 번째 인자로 정규 표현식에 매칭이 되는 문자열을 받는다.
- `→ Boolean`: 두 번째 인자로 받은 문자열이 첫 번째 인자의 정규 표현식을 통과하면 true, 아니면 false를 반환한다.

### 예제
```
R.test(/^x/, 'xyz'); //=> true
R.test(/^y/, 'xyz'); //=> false
```
- `/^x/`는 x로 시작하는 대상인지 확인하는 정규식이다. 주어진 문자열 `'xyz'`는 x로 시작하기 때문에 정규식을 통과하지 못하므로 true를 반환한다.
- `/^y/`는 y로 시작하는 대상인지 확인하는 정규식이다. 주어진 문자열 `'xyz'`는 x로 시작하면 y로 시작하지 않기 때문에 정규식을 통과하지 못하므로 false를 반환한다.

## Reference
- https://ramdajs.com/docs/#test
