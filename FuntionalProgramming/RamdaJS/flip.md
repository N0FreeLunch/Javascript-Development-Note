## flip

> Returns a new function much like the supplied one, except that the first two arguments' order is reversed.
- 주어진 함수와 거의 같은 기능의 새로운 함수를 반환한다. 단 차이가 있다면 처음 두 인자의 순서가 역순이라는 것이다.

## 설명

- 첫 번째 인자와 두번째 인자를 바꿔서 주어진 함수에 인자를 전달하는 것만 다른 나머지는 동일한 함수를 반환한다.
- 첫번째 인자에는 인자를 여러 개 받아 인자를 몇 개를 받든 할당이 되면 평가되어 결과 값을 갖는 함수를 할당한다.

## 문법

```
R.flip(fn): *
```

> `fn`: The function to invoke with its first two parameters reversed.
- `fn`: 처음 두 파라메터가 뒤바뀐 호출할 수 있는 함수를 만든다.
> Returns * The result of invoking `fn` with its first two parameters' order reversed.
- 어떤 타입이든 반환할 수 있다.  

## 표현
```
((a, b, c, …) → z) → (b → a → c → … → z)
```
- `((a, b, c, …) → z)` 첫 번째 인자로 여러 개의 인자를 받아 결과 값을 반환하는 함수를 받는다. 첫 번째 인자로 할당하는 함수의 인자의 갯수는 제한이 없으며 실제 할당되는 함수는 지정된 길이 또는 가변 길이의 인자를 받는 함수가 된다. 또한 인자를 하나를 받든 둘을 받든 몇개를 받든 평가가 되어 결과 값을 갖는 함수를 받는다.
- `(b → a → c → … → z)` 첫 번째 인자를 넣고 반환된 함수를 의미한다. 첫 번째 인자로 받은 함수와 동일하지만 첫 번째 인자와 두 번째 인자의 할당 순서가 달라져 있는 함수이다. 반환된 인자는 커링 되어 있기 때문에 인자를 하나씩 넣어서 평가할 수 있다.

## 예제
```
const mergeThree = (a, b, c) => [].concat(a, b, c);

mergeThree(1, 2, 3); //=> [1, 2, 3]

R.flip(mergeThree)(1, 2, 3); //=> [2, 1, 3]
```
- `(a, b, c) => [].concat(a, b, c)`는 세 개의 인자를 받아서 빈 배열에 추가하는 함수이다.
- [`Array.prototype.concat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) 함수는 가변인자를 받으므로 `mergeThree` 함수는 최대 3개까지 인자를 가변으로 받아서 배열의 원소로 차례로 할당한 배열을 반환하는 함수이다.
- `R.flip`은 주어진 함수의 첫 번째 인자와 두 번째 인자를 바꿔서 할당하도록 변환해 주는 함수이다. 따라서 인자가 `1, 2, 3` 순서로 들어갔지만 `2, 1, 3` 순서로 내부의 `mergeThree` 함수에 넣어지기 때문에 함수의 평가 결과는 `[2, 1, 3]`가 된다.

## References
- https://ramdajs.com/docs/#flip
- https://github.com/ramda/ramda/blob/master/test/flip.js
- https://github.com/ramda/types/blob/develop/types/flip.d.ts
