## replace
> Replace a substring or regex match in a string with a replacement.
- 문자열에서 부분 문자열이나 정규표현식에 매칭된 문자열을 대체 문자로 바꾼다.

> The first two parameters correspond to the parameters of the String.prototype.replace() function, so the second parameter can also be a function.
- (replace 함수의 3개의 파라메터 중에서) 처음 두 파라메터는 String.prototype.replace() 함수의 파라메터를 따른다.

###

### 표현
```
RegExp|String → String → String → String
```
- `RegExp|String →`: 첫 번째 인자로 패턴(문자열 또는 정규 표현식)을 받는다.
- `→ String →`: 두 번째 인자로 패턴 대신에 대체할 문자열을 받는다.
- `→ String →`: 세 번째 인자로 대상 문자열을 받는다.
- `→ String`: 대상 문자열에서 패턴에 해당하는 값을 대체 문자로 바꾼다.

### 예제
```
R.replace('foo', 'bar', 'foo foo foo'); //=> 'bar foo foo'
R.replace(/foo/, 'bar', 'foo foo foo'); //=> 'bar foo foo'

// Use the "g" (global) flag to replace all occurrences:
R.replace(/foo/g, 'bar', 'foo foo foo'); //=> 'bar bar bar'
```
- 'foo foo foo'에서 가장 먼저 나오는 'foo'를 선택한 뒤 'bar'으로 바꾼다. 따라서 'bar foo foo'가 된다.
- 'foo foo foo'에서 `/foo/`에 매칭되는 대상인 `foo`를 선택한 뒤 `bar`으로 바꾼다. 따라서 'bar foo foo'가 된다.
- 'foo foo foo'에서 `/foo/g`에 매칭되는 대상인 `foo` `foo` `foo`를 선택한 뒤 `bar`으로 바꾼다. 따라서 'bar bar bar'가 된다.

## Reference
- https://ramdajs.com/docs/#replace
