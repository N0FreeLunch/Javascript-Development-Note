## times
> Calls an input function n times, returning an array containing the results of those function calls.
- 입력된 함수를 n번 반복 호출한다. 함수 호출들의 결과들을 갖는 배열을 반환한다.

> fn is passed one argument: The current value of n, which begins at 0 and is gradually incremented to n - 1.
- fn은 하나의 인자를 전달 받으며, 순회 중의 n의 값은, 0부터 시작하여 (순회 번째에 해당하는 n에 대해) n - 1 값으로 (순회를 거듭할 수록 n이 증가하므로) 점점 증가한다.

> See also repeat.

### 설명

### 표현
```
(Number → a) → Number → [a]
```
- `(Number → a) →`: 
- `→ Number →`: 
- `→ [a]`: 

### 예제
```js
R.times(R.identity, 5); //=> [0, 1, 2, 3, 4]
```

## Reference
- https://ramdajs.com/docs/#times
