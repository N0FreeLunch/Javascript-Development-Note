## chain
> chain maps a function over a list and concatenates the results. chain is also known as flatMap in some libraries.
- 체인은 리스트가 가진 원소 각각에 대해 동일한 하나의 함수를 매핑하고 반환된 각각의 배열을 하나의 배열로 연결한 결과를 반환한다. 일부 라이브러리에서는 flatMap으로 알려져 있다.
> Dispatches to the chain method of the second argument, if present, according to the FantasyLand Chain spec.
- 만약 두 번째 인자가 존재한다면 `FantasyLand`의 체인 사양에 맞게 체인메소드의 두 번째 인자에 대상(리스트 또는 함수)을 전달하여 평가한다.
> If second argument is a function, chain(f, g)(x) is equivalent to f(g(x), x).
- 두 번째 인자가 함수인 경우에는 `chain(f, g)(x)`는 `f(g(x), x)`와 동일하다.
> Acts as a transducer if a transformer is given in list position.

## 설명 

## 표현
```
Chain m => (a → m b) → m a → m b
```

## 예제
```
const duplicate = n => [n, n];
R.chain(duplicate, [1, 2, 3]); //=> [1, 1, 2, 2, 3, 3]

R.chain(R.append, R.head)([1, 2, 3]); //=> [1, 2, 3, 1]
```
- `R.chain(duplicate, [1, 2, 3])`는 첫 번째 인자로 함수, 두 번째 인자로 리스트를 받았다. 이 경우 `chain` 함수는 `map`함수의 방식으로 `duplicate` 함수에 리스트의 각 원소를 전달하여 실행한 결과를 `duplicate(1)`, `duplicate(2)`, `duplicate(3)`으로 가지며 이 결과는 `[1,1]`, `[2,2]`, `[3,3]`이 된다. `chain`은 배열의 각각의 결과를 연결한 값을 반환하므로 `[1, 1, 2, 2, 3, 3]`을 반환하게 된다.
- `R.chain(R.append, R.head)([1, 2, 3])`는 첫 번째 인자로 함수, 두 번째 인자로도 함수를 받았다. 두 번째 인자로 리스트를 받았을 경우에는 첫 번째 인자로 받은 함수에 리스트의 각 원소를 할당했으나 함수는 리스트가 아니므로 원소를 갖지 못한다. 그래서 두 번째 함수를 첫 번째 함수의 인자에 그대로 전달한다. 첫 번째 함수를 f, 두 번째 함수를 g, 두 번째 인자가 함수가 아닌 리스트의 경우 리스트의 원소를 `Xn(x1, x2, x3 ...)`라고 했을 때, 두 번째 인자가 리스트의 경우는 `f(x1)`, `f(x2)`, `f(x3)`를 연결한 결과가 되었던 반면, 두 번째 인자가 함수인 경우는 `f(g(x), x)`의 원칙에 따라 `R.append(R.head(x), x)`가 된다. 이 반환된 함수에 리스트 인자를 할당하여 `R.append(R.head(x), x)([1,2,3])`이 되므로 `R.append(R.head([1,2,3]), [1,2,3])`가 된다. 따라서 결과 값은 주어진 리스트에서 첫 번째 원소를 뽑는 `R.head([1,2,3])`에 의해 `1`을 반환, `R.append(1, [1,2,3])`에 따라 `[1,2,3,4]`를 반환한다.

## Reference
- https://ramdajs.com/docs/#chain
- https://github.com/fantasyland/fantasy-land#chain
