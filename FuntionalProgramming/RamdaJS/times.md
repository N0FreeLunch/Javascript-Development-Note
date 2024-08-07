## times
> Calls an input function n times, returning an array containing the results of those function calls.
- 입력된 함수를 n번 반복 호출한다. 함수 호출들의 결과들을 갖는 배열을 반환한다.

> fn is passed one argument: The current value of n, which begins at 0 and is gradually incremented to n - 1.
- fn은 하나의 인자를 전달 받으며, 순회 중의 n의 값은, 0부터 시작하여 (순회 번째에 해당하는 n에 대해) n - 1 값으로 (순회를 거듭할 수록 n이 증가하므로) 점점 증가한다.

> See also repeat.

### 설명
- 함수와 횟수(n)를 받아 함수를 주어진 횟수만큼 호출한다. 호출할 때는 0부터 n-1 까지의 수를 차례로 주어진 함수의 인자로 전달한다.
- 함수 fn에 대해 `[fn(0), fn(1), fn(2), fn(3), fn(4), ..., fn(n-3), fn(n-2), fn(n-1)]`의 형태의 결과 값을 갖게 된다.

### 표현
```
(Number → a) → Number → [a]
```
- `(Number → a) →`: 첫 번째 인자로 수를 인자로 하여 어떤 타입 파라메터 a의 값을 반환하는 함수를 받는다.
- `→ Number →`: 두 번째 인자로 횟수를 받는다. 정확히는 0 이상의 정수 값을 받는다.
- `→ [a]`: 두 번째 인자로 받은 횟수 만큼을 첫 번째 인자로 받은 함수의 인자에 0부터 1씩 증가하는 값을 반복하며 전달한 결과들을 나열한 배열을 반환한다.

### 예제
```js
R.times(R.identity, 5); //=> [0, 1, 2, 3, 4]
```
- 0부터 +1씩 증가하는 값을 5번 반복하여 콜백함수인 `R.identity`에 인자를 전달한다.
- `R.identity(0)`, `R.identity(1)`, `R.identity(2)`, `R.identity(3)`, `R.identity(4)`가 된다.
- 이들을 나열한 배열을 반환하므로 `[0, 1, 2, 3, 4]`가 된다.

## Reference
- https://ramdajs.com/docs/#times
