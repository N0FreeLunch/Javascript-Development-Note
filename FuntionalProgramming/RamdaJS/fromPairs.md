## fromPairs

> Creates a new object from a list key-value pairs. If a key appears in multiple pairs, the rightmost pair is included in the object.
- 키-벨류 쌍의 리스트로 부터 새로운 오브젝트를 생성한다.
> See also [toPairs](./toPairs.md), [pair](./pair.md).

## 설명

- 배열의 원소로 0번째 인덱스가 프로퍼티명이고 1번째 인덱스가 값인 배열을 받는다.
- 각각의 원소는 오브젝트의 프로퍼티로 변환된다.
- 주어진 배열의 모든 배열 원소가 오브젝트의 프로퍼티로 변환 되면 새로 만들어진 오브젝트를 반환한다.

## 문법

```
R.fromPairs(pairs): Object
```
> `pairs`: An array of two-element arrays that will be the keys and values of the output object.
- `pairs`: 두 요소(`[a1, b1]`, `[a2, b2]`, `[a3, b3]` ...) 배열의 배열로, 출력할 오브젝트의 키들과 값들이 된다. 
> Returns Object The object made by pairing up `keys` and `values`.
- Object를 반환한다. 이 오브젝트는 `keys`와 `values` 짝을 짓는 것에 의해 만들어진다.

## 표현

```
[[k,v]] → {k: v}
```
- `[[k,v]] →`: 배열의 원소로 크기가 2인 배열로 지정하는데 원소배열의 첫번째 인덱스(`k`)를 키로하고 두번째 인덱스(`v`)를 벨류로 하는 원소배열이 나열된 배열을 받는다.
- `→ {k: v}`: 배열에 지정한 키와 벨류를 오브젝트의 키와 벨류로 만든 오브젝트를 반환한다.

## 예제

```js
R.fromPairs([['a', 1], ['b', 2], ['c', 3]]); //=> {a: 1, b: 2, c: 3}
```
- `['a', 1]` 프로퍼티 a를 만들고 값을 1로 만들며, `['b', 2]` 프로퍼티 b를 만들고 값을 2로 만들며, 프로퍼티 c를 만들고 값을 3으로 하는 오브젝트를 반환하므로 결과값은 `{a: 1, b: 2, c: 3}`이다.

## References

- https://ramdajs.com/docs/#fromPairs
- https://github.com/ramda/ramda/blob/master/test/fromPairs.js
- https://github.com/ramda/types/blob/develop/types/fromPairs.d.ts
