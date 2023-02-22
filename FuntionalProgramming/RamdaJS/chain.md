## chain
> chain maps a function over a list and concatenates the results. chain is also known as flatMap in some libraries.
- 체인은 리스트가 가진 원소 각각에 대해 동일한 하나의 함수를 매핑하고 배열의 중첩을 제거한 결과를 반환한다. 일부 라이브러리에서는 flatMap으로 알려져 있다.
> Dispatches to the chain method of the second argument, if present, according to the FantasyLand Chain spec.
- 만약 두 번째 인자가 존재한다면 `FantasyLand`의 체인 사양에 맞게 체인메소드의 두 번째 인자에 대상(리스트 또는 함수)을 전달한다.
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


## Reference
- https://ramdajs.com/docs/#chain
