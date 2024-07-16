## take
> Returns the first n elements of the given list, string, or transducer/transformer (or object with a take method).
- 주어진 대상에서 처음 n개의 원소를 반환한다. 대상으로는 리스트, 문자열, transducer/transformer, take 메소드를 갖는 object가 가능하다.

> Dispatches to the take method of the second argument, if present.
- 두 번째 인자에 take 메소드가 있다면, take 메소드를 발동한다.

> See also drop.

### 설명

### 표현
```
Number → [a] → [a]
Number → String → String
```

### 예제
```js
R.take(1, ['foo', 'bar', 'baz']); //=> ['foo']
R.take(2, ['foo', 'bar', 'baz']); //=> ['foo', 'bar']
R.take(3, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.take(4, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.take(3, 'ramda');               //=> 'ram'
```
- 

```js
const personnel = [
  'Dave Brubeck',
  'Paul Desmond',
  'Eugene Wright',
  'Joe Morello',
  'Gerry Mulligan',
  'Bob Bates',
  'Joe Dodge',
  'Ron Crotty'
];

const takeFive = R.take(5);
takeFive(personnel);
//=> ['Dave Brubeck', 'Paul Desmond', 'Eugene Wright', 'Joe Morello', 'Gerry Mulligan']
```

## Reference
- https://ramdajs.com/docs/#take
