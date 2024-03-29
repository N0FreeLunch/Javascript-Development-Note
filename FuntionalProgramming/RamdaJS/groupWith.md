## groupWith
> Takes a list and returns a list of lists where each sublist's elements are all satisfied pairwise comparison according to the provided function. Only adjacent elements are passed to the comparison function.

## 표현
```
((a, a) → Boolean) → [a] → [[a]]
```
- `((a, a) → Boolean) →` 첫 번째 인자로는 동일 종류 인자를 두 개 받아서 참 거짓을 반환하는 술어함수를 받는다.
- `→ [a] →` 두 번째 인자는 주어진 술어함수의 두 인자로 할당될 수 있는 종류의 원소로 이뤄진 배열을 받는다.
- `→ [[a]]` 반환 값으로 연속된 두 원소가 주어진 술어함수의 인자로 할당될 때 거짓을 반환하거나 첫 번째 원소이면 새로운 배열에 넣고, 참을 반환하는 경우 기존 배열에 넣어 나열하므로 모든 원소가 배열인 배열을 반환한다.

## 설명
- `groupBy`가 주어진 함수의 반환값이 같은 것 끼리 주어진 배열의 원소들을 분류하는 것에 반해, `groupWith`는 연달아 이어지는 원소들이 주어진 술어함수를 만족하면 하나의 배열의 원소로 묶는 역할을 한다.
- 첫 번째 인자로 술어 함수를 받는다. 이 술어 함수는 인자를 둘 받아서 참 아니면 거짓을 반환한다.
- 두 번째 인자로 주어진 술어함수의 인자로 할당할 수 있는 원소로 이뤄진 배열을 받는다.
- 주어진 배열을 차례로 순회하면서 첫 번째 원소는 새로운 배열에 넣고, 다음으로는 연속한 두 원소가 주어진 술어함수의 인자로 할당 될 때 거짓이면 새로운 배열을 만들어 두 번째 원소를 넣고 술어함수가 참이면 기존 배열에 두 번째 원소를 넣어 나열한 결과를 배열로 반환한다.

## 예제
```
R.groupWith(R.equals, [0, 1, 1, 2, 3, 5, 8, 13, 21])
//=> [[0], [1, 1], [2], [3], [5], [8], [13], [21]]

R.groupWith((a, b) => a + 1 === b, [0, 1, 1, 2, 3, 5, 8, 13, 21])
//=> [[0, 1], [1, 2, 3], [5], [8], [13], [21]]

R.groupWith((a, b) => a % 2 === b % 2, [0, 1, 1, 2, 3, 5, 8, 13, 21])
//=> [[0], [1, 1], [2], [3, 5], [8], [13, 21]]

const isVowel = R.test(/^[aeiou]$/i);
R.groupWith(R.eqBy(isVowel), 'aestiou')
//=> ['ae', 'st', 'iou']
```
- 술어함수 `R.equals`에 대해 0은 첫 번째 원소이므로 배열에 넣어서 `[0]`이며, 0과 1은 주어진 술어함수를 만족하지 않으므로 1은 새로운 배열에 넣어서 `[1]`이며, 1과 1은 주어진 술어함수를 만족하므로 기존의 배열에 추가해서 `[1, 1]`이며, 1과 2는 주어진 술어함수를 만족하지 않으므로 새로운 배열에 넣어서 `[2]`이며 2와 3은 주어진 술어함수를 만족하지 않으므로 새로운 배열에 넣어서 `[3]`이며 3과 5는 주어진 술어함수를 만족하지 않으므로 새로운 배열에 넣어서 `[5]`이며, 5와 8은 주어진 술어함수를 만족하지 않으므로 새로운 배열에 넣어서 `[8]`이며, 8과 13은 주어진 술어함수를 만족하지 않으므로 새로운 배열에 넣어서 `[13]`이며, 13과 21은 주어진 술어함수를 만족하지 않으므로 새로운 배열에 넣어서 `21`이다. 따라서 결과 값은 ` [[0], [1, 1], [2], [3], [5], [8], [13], [21]]`가 된다.
- 술어함수 `((a, b) => a + 1 === b`에 대해 0은 첫 번째 원소이므로 배열에 넣어서 `[0]`, 0과 1은 주어진 술어함수를 만족하므로 기존 배열에 넣어서 `[0, 1]`이며, 1과 1은 주어진 술어 함수를 만족하지 않으므로 새로운 배열에 넣어서 `[1]`이며, 1과 2는 주어진 술어함수를 만족하므로 기존 배열에 넣어서 `[1, 2]`이며, 2와 3은 주어진 술어 함수를 만족하므로 기존 배열에 넣어서 `[1, 2, 3]`이며, 3과 5는 주어진 술어함수를 만족하지 않으므로 새로운 배열에 넣어서 `[5]`이며 5와 8은 주어진 술어함수를 만족하지 않으므로 새로운 배열을 만들어 `[8]`이며, 8과 13은 술어함수를 만족하지 않으므로 새 배열을 만들어 `[13]`이며, 13과 21은 술어함수를 만족하지 않으므로 새 배열 `[21]`을 반환한다. 따라서 만들어진 배열을 배열 안에 나열하면 `[[0, 1], [1, 2, 3], [5], [8], [13], [21]]`가 된다.
- 술어함수 `(a, b) => a % 2 === b % 2`는 짝수끼리 홀수끼리이면 참 아니면 거짓을 반환하는 함수이다. 0은 첫 번째 원소이므로 새 배열에 넣어서 `[0]`이며 0과 1은 거짓으로 `[1]`이며, 1과 1은 홀수인 참이므로 기존 배열에 추가하여 `[1, 1]`이며, 1과 2는 거짓으로 새 배열인 `[2]`이며, 2와 3은 거짓으로 새 배열인 `[3]`이며, 3과 5는 홀수인 참으로 기존 배열에 추가하여 `[3, 5]`이며, 5와 8은 거짓으로 새 배열 `[8]`이며, 8과 13은 거짓으로 새 배열 `[13]`이며, 13과 21은 홀수인 참으로 기존 배열에 추가하여 `[13, 21]`이 된다. 만들어진 배열들을 나열하면 `[[0], [1, 1], [2], [3, 5], [8], [13, 21]]`이다.
- `R.test`는 첫 번째 인자로 자바스크립트 정규표현식을 두 번째 인자로 문자열을 입력하여 주어진 정규표현을 만족하는지 확인하는 술어함수이다. `R.eqBy`는 첫 번째 인자로 함수를 받고 두 번째 세번째 인자로 첫 번째에 넣은 함수의 인자로 넣어 평가했을 때 두 값이 일치하는지 확인하는 함수이다. `R.eqBy(isVowel)`는 두 인자를 받아 두 인자가 `isVowel`의 정규식을 만족하는 문자열인지 확인한다. `'aestiou'`는 배열에 상당하므로 `a`는 첫 번째 원소이므로 새 배열 `['a']`, `a`와 `e`는 술어함수를 만족하므로 기존 배열에 추가해 `['a', 'e']`, `e`와 `s`는 술어함수를 만족하지 않으므로 새 배열 `['s']`, `s`와 `t`는 술어함수를 만족하므로 기존 배열 `['s', 't']`, t와 i는 술어함수를 만족하지 않으므로 `[i]`이며, `i`와 `o`는 술어함수를 만족하므로 기존 배열에 추가하여 `[i, o]`, `o`와 `u`는 술어함수를 만족하므로 기존 배열에 추가하여 `[i, o, u]`이다. 그런데 문자열이므로 만들어지는 것도 문자열로 만들어진다. 내부적으로는 배열이 아닌 문자열로 로직이 구성된다. 따라서 결과는 `['ae', 'st', 'iou']`이다.

## Reference
- https://ramdajs.com/docs/#groupWith
