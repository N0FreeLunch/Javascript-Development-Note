## test
> Determines whether a given string matches a given regular expression.
- 주어진 정규 표현식에 주어진 문자열이 매칭되는지(정규식을 통과하는 대상이 있는지)를 확인한다.

> See also match.

### 설명
- 정규 표현식과 문자열을 하나 받아, 문자열이 정규식을 통과하면 true, 그렇지 않으면 false를 반환한다.

### 표현
```
RegExp → String → Boolean
```
- `RegExp →`: 첫 번째 인자로 정규 표현식을 받는다. 자바스크립트의 정규 표현식은 오브젝트인데, RegExp 클래스를 사용해서 `new RegExp('^x')`으로도 만들 수 있지만 `/^x/`와 같은 슬레시를 사용한 문법도 지원한다.
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
