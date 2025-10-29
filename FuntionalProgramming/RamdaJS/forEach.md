## forEach

> Iterate over an input list, calling a provided function fn for each element in the list.
- 주어진 리스트 전체를 순회한다. 제공된 함수를 fn이라고 할 때 주어진 리스트에서 각각의 원소를 fn에 전달하여 할당한다.

> fn receives one argument: (value).
- fn은 하나의 인자를 받는다.

> Note: R.forEach does not skip deleted or unassigned indices (sparse arrays), unlike the native Array.prototype.forEach method. For more details on this behavior, see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#Description
- 자바스크립트에 내장된 배열 함수 `Array.prototype.forEach` 메소드와 달리 `R.forEach`는 삭제되었거나 할당되지 않은 색인을 건너 뛰지 않는다. 여기에 대해 더 자세히 알고 싶다면 다음을 참고하자 : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#Description 

> Also note that, unlike Array.prototype.forEach, Ramda's forEach returns the original array. In some libraries this function is named each.
- 또한 주목할만한 점은 `Array.prototype.forEach`와 달리 Ramda의 forEach는 원본 배열을 반환한다. 일부 라이브러리에서는 이 함수를 `each`라는 명칭으로 사용된다.

> Dispatches to the forEach method of the second argument, if present.
- 만약 두 번째 인자의 메소드에 forEach

## 설명

- 첫 번째 인자로 하나의 매개변수를 갖는 함수를 받는다. 이 함수의 반환 값은 있어도 되고 없어도 되며 어떠한 종류든 허용된다.
- 두 번째 인자로 첫 번째 인자로 받은 함수의 인자로 할당될 수 있는 종류의 원소로 이루어진 배열을 받는다.
- 두 번째 인자로 받은 배열의 원소를 첫 번째 함수에 할당하여 함수를 실행하며 반환 값으로는 두 번째로 받은 배열의 원본을 반환한다.
- 자바스크립트에서 배열은 기본적으로 참조로 전달된다. 반환 된 값은 원본 배열을 가리킨다. 대부분의 RamdaJS 함수는 평가된 결과로 새로 만들어지거나 복사된 값을 반환하지만 `forEach`는 예외적으로 원본 배열의 참조를 반환한다.
- 반환 값이 원본 배열이므로 인풋과 아웃풋의 차이가 없다. 그저 순회를 하면서 사이드 이펙트를 만드는 것으로 사용될 뿐이다.

## 문법

```
R.forEach(fn, list): Array
```

> `fn`: The function to invoke. Receives one argument, value.
- `fn`: 호출할 함수이다. (이 함수는 인자로) 하나의 인자 (키는 제외한 리스트의 원소) 값(만) 받는다.
> `list`: The list to iterate over.
- `list`: 순회 처리할 리스트
> Returns Array The original list.
- 배열을 반환한다. 이 배열은 (함수의 인자로 전달된) 원본 리스트이다.

## 표현

```
(a → *) → [a] → [a]
```
- `(a → *) →`: 첫 번째 인자로 하나의 인자를 받는 함수를 받는다. 이 함수의 반환 값은 무엇이든 가능하며 반환값이 없어 `null`을 반환하는 함수도 가능하다.
- ` → [a] →`: 두 번째 인자로 순회할 배열을 받는다. 단 이 배열을 이루는 원소는 첫 번재 인자로 받은 함수의 인자로 할당할 수 있는 종류여야 한다.
- `→ [a]`: 두 번째 인자로 받은 배열을 첫 번째 인자의 함수의 파라메터로 원소를 하나씩 전달해 이를 이용해서 사이드 이펙트를 갖는 연산을 하고 두 번째 인자로 받은 배열의 원본을 반환한다. 복사가 아니다.

## 예제

```js
const printXPlusFive = x => console.log(x + 5);
R.forEach(printXPlusFive, [1, 2, 3]); //=> [1, 2, 3]
// logs 6
// logs 7
// logs 8
```
- `printXPlusFive`는 `console.log`라는 사이드 이펙트를 실행하는 함수이다. 
- 두 번째 인자로 받은 배열의 원소 `1, 2, 3`을 순차적으로 할당하며 로직을 처리한다.
- `console.log`로 해당 로직의 전개와는 관련 없는 사이드 이펙트를 만들어 낼 때 사용한다는 것을 알 수 있다.

## References

- https://ramdajs.com/docs/#forEach
- https://github.com/ramda/ramda/blob/master/test/forEach.js
- https://github.com/ramda/types/blob/develop/types/forEach.d.ts
