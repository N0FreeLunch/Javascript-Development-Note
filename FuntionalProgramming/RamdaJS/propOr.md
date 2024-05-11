## propOr
> Return the specified property of the given non-null object if the property is present and it's value is not null, undefined or NaN.
- null이 아닌 오브젝트가 주어지고, 만약 지정된 프로퍼티가 존재하고 프로퍼티의 값이 null, undefined, null이 아닐 때, 해당 프로퍼티의 값을 반환한다.

> Otherwise the first argument is returned.
- 그렇지 않으면 첫 번째 인자를 반환한다.

### 설명
- 지정한 대상이 존재하지 않을 경우 디폴트 값을 반환하는 prop 함수이다. 이 때 지정한 대상이 존재하지 않는다는 것은, 지정한 프로퍼티가 오브젝트 내에 존재하지 않거나, 대상 프로퍼티가 가진 값이 undefined, null, NaN인 경우에 해당한다.
- 첫 번째 인자로 대상 값이 없을 경우 반환할 디폴트 값을 정한다.
- 두 번째 인자로 대상 오브젝트의 프로퍼티를 지정한다.
- 세 번째 인자로 대상 오브젝트를 받는다.
- 오브젝트에서 지정한 프로퍼티의 값을 반환하며 프로퍼티가 없거나 프로퍼티의 값이 undefined, null, NaN인 경우 첫 번째 인자의 값인 디폴트 값을 반환한다.

### 표현
```
a → String → Object → a
```
- `a → `: 지정한 대상이 존재하지 않을 경우 반환할 값을 정한다.
- `→ String →`: 값을 추출할 프로퍼티를 지정한다.
- `→ Object →`: 대상 오브젝트를 정한다.
- `→ a`: 추출할 대상이 존재하면 해당 값을 반환하고 그렇지 않을 때 첫 번째 인자로 받은 값을 반환한다.

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
- `favoriteWithDefault` 함수는 `R.propOr('Ramda', 'favoriteLibrary')`으로 디폴트 값과, 대상 프로퍼티가 지정되었다. 오브젝트를 하나 받아서 지정한 오브젝트의 프로퍼티가 존재하고 그 프로퍼티의 값이 null, undefined, NaN이 아닐 때 그 값을 반환하고, 그렇지 않으면 디폴트 값을 반환한다. `'favoriteLibrary'`라는 프로퍼티가 존재하지 않으므로 디폴트 값인 `'Ramda'`를 반환한다.

## Reference
- https://ramdajs.com/docs/#propOr
