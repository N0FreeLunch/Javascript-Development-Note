## multiply
> Multiplies two numbers. Equivalent to a * b but curried.
- 두 수를 곱한다. a * b와 동일하지만 커링되어 있다.

## 설명
- 두 개의 수를 인자로 차례로 받아서 두 수의 곱을 반환한다.
- 함수의 인자로 곱할 수를 차례롤 받는데, 인자를 하나만 받는다면 자동으로 커링된다.
- 곱할 두 수는 인자에 할당하는 순서를 바꾸어도 동일한 결과를 갖기 때문에 한 인자를 비워두고 두 번째 인자를 받을 필요는 없다.

## 표현
```
Number → Number → Number
```
- `Number → ` 첫 번째 인자로 수를 받는다.
- `→ Number →` 두 번째 인자로 수를 받는다.
- `→ Number` 인자로 받은 두 수의 곱을 반환한다.

## 예제
```js
const double = R.multiply(2);
const triple = R.multiply(3);
double(3);       //=>  6
triple(4);       //=> 12
R.multiply(2, 5);  //=> 10
```
- `R.multiply(2)`는 인자를 하나 더 받아서 2를 곱하라는 커링된 함수이다. 따라서 `double` 이라는 이름의 함수명을 사용하였으며 이 함수에 인자를 하나 할당하면 2가 곱해진 결과를 얻는다.
- `R.multiply(3)`는 인자를 하나 더 받아서 3을 곱하라는 커링된 함수이다. 따라서 `triple` 이라는 이름의 함수명을 사용하였으며 이 함수에 인자를 하나 할당하면 3이 곱해진 결과를 얻는다.
- `double(3)`는 2에 3을 곱한 값이므로 6이다.
- `triple(4)`는 2에 4가 곱해진 값이므로 6이다.
- `R.multiply(2, 5)`와 같이 인자를 두 개 할당하면 결과값을 만들어 내기 위한 인자의 수가 충족되므로 커링되지 않고 2와 5의 곱을 바로 반환한다.

## Reference
- https://ramdajs.com/docs/#multiply
