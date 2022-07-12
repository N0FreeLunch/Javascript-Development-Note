## call



## 표현
```
((*… → a), *…) → a
```

## 설명



## 예제
```
R.call(R.add, 1, 2); //=> 3
```
- `R.call(R.add, 1, 2);` `R.call`이란 함수는 첫 번째 인자로 함수를 받고, 두 번째 인자 부터는 첫 번째 인자로 받은 함수의 인자로 집어 넣을 인자를 받는다. `R.add`에 인자 `1`과 `2`를 넣는다는 뜻이다.
```
const indentN = R.pipe(
  R.repeat(' '),
  R.join(''),
  R.replace(/^(?!$)/gm)
);
```
- `R.repeat(' ')` 는 원소가 배열에서 `' '`라는 동일한 원소를 지정한 수 만큼을 넣은 배열을 만든다.
- `R.join('')`은 배열의 원소 사이를 `''`으로 연결한 단일 문자열으로 만든다.
- `R.replace(/^(?!$)/gm)`는 문자열의 마지막이 아닌 경우 문자열의 마지막을 입력된 값으로 치환하겠다는 의미 ([Assertions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Assertions)에서 `x(?!y)`를 검색하자.)

```
const format = R.converge(
  R.call,
  [
    R.pipe(R.prop('indent'), indentN),
    R.prop('value')
  ]
);

```
```
format({indent: 2, value: 'foo\nbar\nbaz\n'}); //=> '  foo\n  bar\n  baz\n'
```

## Reference
- https://ramdajs.com/docs/#call
