## match
> Tests a regular expression against a String.

> Note that this function will return an empty array when there are no matches.

> This differs from String.prototype.match which returns null when there are no matches.

## 설명
- 정규 표현식 객체와 문자열을 받아 문자열에서 정규식에 매칭되는 부분을 반환한다. 매칭되지 않는 경우 undefined를 반환한다.

## 표현
```
RegExp → String → [String | Undefined]
```
- `RegExp →` 첫 번째 인자로 정규식을 받는다. 정규식 타입을 받기 때문에 `/정규식 표현/` 또는 `new RegExp(/정규식표현/, '플레그')`등의 정규식 오브젝트를 넣어줘야 한다.
- `→ String →` 두 번째로 첫 번째 인자로 받은 정규식을 적용할 문자열을 지정한다. 
- `→ [String | Undefined]` 주어진 문자열에 주어진 정규식에 매칭되는 문자열이 있다면 해당 문자열을 반환하고 매칭되는 문자열이 없다면 `undefined`를 반환한다.

## 예제
```
R.match(/([a-z]a)/g, 'bananas'); //=> ['ba', 'na', 'na']
R.match(/a/, 'b'); //=> []
R.match(/a/, null); //=> TypeError: null does not have a method named "match"
```
- 설명은 단순하므로 생략한다.

## Reference
- https://ramdajs.com/docs/#match
