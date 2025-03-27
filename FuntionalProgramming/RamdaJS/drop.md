# drop

> Returns all but the first n elements of the given list, string, or transducer/transformer (or object with a drop method).
- 주어진 리스트, 문자열 또는 변환기(transducer) 및 변형기(transformer) (또는 drop 메소드를 가진 오브젝트)에서 처음(first) n개 원소를 제외한 모든 원소를 반환한다.
> Dispatches to the drop method of the second argument, if present.
- 만약 두번째 인자에 drop 메소드가 존재하면 drop 메소드를 실행한다.
> See also [take](./take.md), [transduce](./transduce.md), [dropLast](./dropLast.md), [dropWhile](./dropWhile).

## 설명

- 첫 번째 인자로 배열의 몇 번째 인덱스까지 지울 것인지 정한다. 지정한 수가 배열의 길이를 이상인 경우 모든 인덱스가 삭제되며 빈 배열이 반환된다.
- 두 번째 인자로 대상 배열을 지정한다. 배열이 아닌 문자열이 오면 문자열의 n번째 문자까지 지운 문자열을 반환한다.
- 두 번째 인자의 배열 또는 문자열에 drop 메소드를 추가해 주면 drop 메소드를 실행하여 지운다.

## 문법

```
R.drop(n, list): *
```
> `n`
- `n`: 드롭할 원소의 수
> `list`
- `list`: 드롭 할 리스트
> Returns * A copy of list without the first `n` elements
- 처음 n개의 원소가 없는 리스트의 복사본(과 동일한 타입인) *를 반환한다. 


## 표현

```
Number → [a] → [a]
```
- `Number →`: 첫 번째 인자로 몇 번째 인덱스까지 지울 것인지 정하는 수를 지정한다.
- `→ [a] →`: 두 번째 인자로 배열을 받는다.
- `→ [a]`: 두 번째 인자의 배열에서 첫 번째 인자로 지정한 수 만큼의 원소를 앞에서 부터 제거한 복사본의 배열을 반환한다.

```
Number → String → String
```
- `Number →`: 첫 번째 인자로 몇 번째 인덱스까지 지울 것인지 정하는 수를 지정한다.
- `→ String →`:두 번째 인자로 문자열을 받는다.
- `→ String`: 두 번째 인자의 문자열에서 첫 번째 인자로 지정한 수 만큼의 문자를 앞에서 부터 제거한 복사본의 문자열을 반환한다.

## 예제

```js
R.drop(1, ['foo', 'bar', 'baz']); //=> ['bar', 'baz']
R.drop(2, ['foo', 'bar', 'baz']); //=> ['baz']
R.drop(3, ['foo', 'bar', 'baz']); //=> []
R.drop(4, ['foo', 'bar', 'baz']); //=> []
R.drop(3, 'ramda');               //=> 'da'
```
- 주어진 배열에서 첫 번째 인덱스까지의 원소를 제거한 결과를 반환한다. `['foo', 'bar', 'baz']`에서 첫번째 인덱스 `'foo'`를 제거하여 `['bar', 'baz']`가 된다.
- 주어진 배열에서 두 번째 인덱스까지의 원소를 제거한 결과를 반환한다. `['foo', 'bar', 'baz']`에서 두번째 인덱스까지 `'foo'`, `'bar'`를 제거하여 `['baz']`가 된다.
- 주어진 배열에서 세 번째 인덱스까지의 원소를 제거한 결과를 반환하므로 빈 배열이 반환된다.
- 주어진 배열에서 네 번째 인덱스까지의 원소를 제거한 결과를 반환하는데 4번째 인덱스가 없으므로 모든 원소를 제거한 빈 배열이 반환된다.
- 문자열의 3번째 자리까지 제거한 문자를 반환하므로 `'da'`가 반환된다.

```js
const text = 'ramda';
text.__proto__.drop = function (n) {
  const sliced = this.slice(n, this.length);
//  return 'hello';
  return sliced;
};

R.drop(3, text);
```

- `text`라는 문자열에 `drop` 메소드를 추가하였다. `text.drop(2)`을 하면 `mda`가 반환된다.
- `R.drop(3, text)`의 코드를 실행할 때 `text`에 `drop` 메소드가 정의되어 있기 때문에, `drop` 메소드를 실행한다. 주석이 처리된 `return 'hello'`를 실행하면, `R.drop(3, text)`의 결과가 `'hello'`가 되는 것을 통해서 `R.drop`에 의해 데이터가 잘리는 것이 아니라, `drop` 메소드에 의해 데이터가 잘린다는 것을 알 수 있다. `drop` 메소드를 정의하면 문자열, 배열 뿐만 아니라 다른 개념에 대해서도 동일하게 `R.drop`으로 데이터를 `drop` 할 수 있다.

## References

- https://ramdajs.com/docs/#drop
- https://github.com/ramda/ramda/blob/master/test/drop.js
- https://github.com/ramda/types/blob/develop/types/drop.d.ts
