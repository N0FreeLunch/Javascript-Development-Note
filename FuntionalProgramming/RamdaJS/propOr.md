## propOr
> Return the specified property of the given non-null object if the property is present and it's value is not null, undefined or NaN.
- null이 아닌 오브젝트가 주어지고, 만약 지정된 프로퍼티가 존재하고 프로퍼티의 값이 null, undefined, null이 아닐 때, 해당 프로퍼티의 값을 반환한다.

> Otherwise the first argument is returned.

### 설명

### 표현
```
a → String → Object → a
```

### 예제
```js
const alice = {
  name: 'ALICE',
  age: 101
};
const favorite = R.prop('favoriteLibrary');
const favoriteWithDefault = R.propOr('Ramda', 'favoriteLibrary');

favorite(alice);  //=> undefined
favoriteWithDefault(alice);  //=> 'Ramda'
```
- `favorite` 함수는 `R.prop('favoriteLibrary')`으로 오브젝트를 하나 받아서 `'favoriteLibrary'` 프로퍼티의 값을 반환하는 함수이다. 이 지정한 프로퍼티가 존재하지 않는 `alice`와 같은 오브젝트를 인자로 받았을 때 `undefined`를 반환한다.
- `favoriteWithDefault` 함수는 `R.propOr('Ramda', 'favoriteLibrary')`으로 디폴트 값과, 대상 프로퍼티가 지정되었다. 오브젝트를 하나 받아서 지정한 오브젝트의 프로퍼티가 존재하고 그 프로퍼티의 값이 null, undefined, null이 아닐 때 그 값을 반환하고, 그렇지 않으면 디폴트 값을 반환한다.

## Reference
- https://ramdajs.com/docs/#propOr
