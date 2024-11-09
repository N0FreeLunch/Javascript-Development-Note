## clamp
> Restricts a number to be within a range.
- 지정한 수를 일정한 범위 내로 제한한다.

> Also works for other ordered types such as Strings and Dates.
- 또한 문자열이나 날짜와 같은 순서가 있는 타입들에도 적용된다.

### 설명
- 범위를 지정하고 지정한 값이 범위 내에 있다면 해당 값을 반환하고 그렇지 않으면 지정된 범위 내에서 지정한 값에 가장 가까운 값을 반환한다.
- clamp는 고정시킨다는 의미로 수학에서는 어떤 범위 내로 값을 제한한다는 의미를 갖는다. 값이 범위 내에 있으면 해당 값을, 값이 범위 밖에 있으면 그 값에 가까운 최대값 또는 최소값을 반환한다.
- 첫 번째 인자로 최소값을 받는다. 두 번째 인자로 최대값을 받는다. 세 번째 인자로 값을 받아, 세 번째 인자가 첫 번째 인자와 두 번째 인자 내의 범위라면 세 번째 인자를 그대로 반환하지만 그렇지 않으면 세 번째 인자와 가장 가까운 값을 첫 번째 인자 또는 두 번째 인자가 반환한다.

### 문법
```
R.clamp(fn): function
```
> `fn`: The function to wrap.
- `fn`: 레핑할 함수
> Returns function A new function wrapping `fn`. The new function is guaranteed to be of arity 2.
- `fn`을 레핑한 새로운 함수를 반환한다. 새로운 함수의 인자의 갯수는 2개로 보장된다.

### 표현
```
Ord a => a → a → a → a
```
- `Ord a =>`: 순서가 있는 타입 `a`에 대해
- `a →`: 첫 번째 인자로 순서가 있는 어떤 값을 받고
- `→ a →`: 두 번째 인자로 순서가 있는 어떤 값을 받고
- `→ a →`: 세 번째 인자로 순서가 있는 어떤 값을 받고
- `→ a`: 세 개의 값이 모두 할당되면 세 번째 값이 첫 번재 인자 보다 크고 두 번째 인자보다 작다면 세 번째 인자를, 그렇지 않으면 첫 번째 인자와 두 번째 인자 중에서 세 번째 인자에 가까운 값을 반환한다.

## 예제
```js
R.clamp(1, 10, -5) // => 1
```
- 최소값을 1로, 최대값을 10으로 설정하였는데 `-5`가 할당되었으므로 범위 내의 값 중에 `-5`에 가장 가까운 값인 1이 반환된다.

```js
R.clamp(1, 10, 15) // => 10
```
- 최소값을 1, 최대값을 10으로 설정하였는데 `15`가 할당되었으므로 범위 내의 값 중에 `15`에 가장 가까운 값인 10이 반환된다.

```js
R.clamp(1, 10, 4)  // => 4
```
- 최소값을 1, 최대값을 10으로 설정하였는데 `4`가 할당되었으므로 범위 내에 속한다. `4`에 가장 가까운 값은 `4`이므로 `4`가 반환된다.

## References
- https://ramdajs.com/docs/#clamp
- https://github.com/ramda/ramda/blob/master/test/clamp.js
- https://github.com/ramda/types/blob/develop/types/clamp.d.ts
