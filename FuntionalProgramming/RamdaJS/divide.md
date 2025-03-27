# divide

> Divides two numbers. Equivalent to a / b.
- 두 수를 나눈다. a/b와 동일하다.
> See also [multiply](./multiply.md).

## 설명

- '첫 번째 인자' 나누기 '두 번째 인자'의 결과를 반환한다.

## 문법

```
R.divide(a, b): Number
```
> `a`: The first value.
- `a`: 첫 번째 값
> `b`: The second value.
- `b`: 두 번째 값
> Returns Number The result of `a / b`.
- `a / b`의 결과 Number를 반환한다.

## 표현

```
Number → Number → Number
```

- `Number →`: 첫 번째 인자로는 피제수(분할 대상, 나눔을 당하는 수)
- `→ Number →`: 두 번째 인자로는 제수(분할 단위, 나누는 수)
- `→ Number`: 반환 결과는 나눈 결과 값이다.

## 예제

```js
R.divide(71, 100); //=> 0.71
```
- `R.divide(71, 100)` 71/100 = 0.71

```js
const half = R.divide(R.__, 2);
half(42); //=> 21
```
- `R.divide(R.__, 2)`는 어떤 수를 2로 나눈다는 의미 `half`함수에 수를 넣으면 반으로 된다. 함수가 어떤 기능을 하는지 알기 쉽도록 half라는 명칭을 부여하였다.

```js
const reciprocal = R.divide(1);
reciprocal(4);   //=> 0.25
```
- `R.divide(1)` RamdaJS에서 함수는 커링이 적용되어 있기 때문에 `reciprocal`함수가 인자를 받으면 1을 인자로 받은 수 만큼으로 나누는 함수가 됨
- `reciprocal(4);`는 1을 4로 나눈다는 의미, `reciprocal`라는 반비례를 의미하는 단어로 함수명을 지었다.

## References
- https://ramdajs.com/docs/#divide
- https://github.com/ramda/ramda/blob/master/test/divide.js
- https://github.com/ramda/types/blob/develop/types/divide.d.ts
