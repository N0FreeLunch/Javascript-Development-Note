## init
> Returns all but the last element of the given list or string.
- 주어진 리스트 또는 배열의 마지막 원소를 제외한 모두를 반환한다.

## 표현
```
[a] → [a]
String → String
```
- `[a] →` 배열을 받으면 배열의 마지막 원소를 제외한 배열을 반환하므로 여전히 `→ [a]` 배열이 된다.
- `String →` 문자열을 받으면 문자열의 마지막 원소인 마지막 문자를 제외한 문자열을 반환하므로 `→ String` 배열이 된다.

## 설명
- 하나의 배열 또는 한 단위의 문자열을 인자로 받아서 마지막 원소 또는 마지막 문자를 제외한 결과를 반환한다.
- 빈 배열 또는 빈 문자열이 인자로 주어지면 빈 배열이면 빈 배열, 빈 문자열이면 빈 문자열을 반환한다.

## 예제
```
R.init([1, 2, 3]);  //=> [1, 2]
R.init([1, 2]);     //=> [1]
R.init([1]);        //=> []
R.init([]);         //=> []

R.init('abc');  //=> 'ab'
R.init('ab');   //=> 'a'
R.init('a');    //=> ''
R.init('');     //=> ''
```

## Refernece
- https://ramdajs.com/docs/#init
