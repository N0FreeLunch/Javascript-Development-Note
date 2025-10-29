# addIndexRight

> As with addIndex, addIndexRight creates a new list iteration function from an existing one by adding two new parameters to its callback function: the current index, and the entire list.

> Unlike addIndex, addIndexRight iterates from the right to the left.

## 설명

## 문법

```
R.addIndexRight(fn): function
```
> `fn` : A list iteration function that does not pass index or list to its callback
> Returns function An altered list iteration function that passes (item, index, list) to its callback

## 표현

```
((a … → b) … → [a] → *) → (a …, Int, [a] → b) … → [a] → *)
```

## 예시

```js
const revmap = (fn, ary) => R.map(fn, R.reverse(ary));
const revmapIndexed = R.addIndexRight(revmap);
revmapIndexed((val, idx) => idx + '-' + val, ['f', 'o', 'o', 'b', 'a', 'r']);
//=> [ '5-r', '4-a', '3-b', '2-o', '1-o', '0-f' ]
```

## References

- https://ramdajs.com/docs/#addIndexRight
