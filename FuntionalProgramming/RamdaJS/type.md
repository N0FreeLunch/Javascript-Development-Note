## type
> Gives a single-word string description of the (native) type of a value, returning such answers as 'Object', 'Number', 'Array', or 'Null'.
- 값이 갖는 (네이티브) 타입에 관한 설명 한 단어의 설명을 제공한다. 'Object', 'Number', 'Array', 'Null'과 같은 답변을 반환한다.
> Does not attempt to distinguish user Object types any further, reporting them all as 'Object'.
- 사용자 정의의 Object 타입은 더 이상 구분하지 않고 모두 'Object'로 보고한다.

### 설명
- 자바스크립트 값의 네이티브 타입 문자열을 반환한다. 자바스크립트에서 [typeof](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/typeof) 키워드의 역할과 비슷한데, typeof 보다 좀 더 상세한 분류를 제공한다. typeof는 null, 배열, 정규표현식에 대해서는 object를 반환하고 비동기 함수로 function을 반환하지만, `R.type()`은 Null, Array, RegExp, AsyncFunction라는 상세한 분류를 제공한다.
- 어디까지나 이런 분류는 네이티브 타입을 구분할 수 있으며, 사용자 정의 오브젝트에 대한 구분은 하지 못한다.
- 아마도 자바스크립트 판타지렌드에서 활용할 수 있는 타입을 구분할 수 있는 용도로 쓰이지 않을까 추측된다.

### 표현
```
* → String
```
- `* →`: 타입에 관계 없이 임의의 값 하나를 받는다.
- `→ String`: 해당 값의 타입을 문자열로 반환한다.

### 예제
```js
R.type({}); //=> "Object"
R.type(1); //=> "Number"
R.type(false); //=> "Boolean"
R.type('s'); //=> "String"
R.type(null); //=> "Null"
R.type([]); //=> "Array"
R.type(/[A-z]/); //=> "RegExp"
R.type(() => {}); //=> "Function"
R.type(async () => {}); //=> "AsyncFunction"
R.type(undefined); //=> "Undefined"
R.type(BigInt(123)); //=> "BigInt"
```

```Js
typeof {}; //=> "object"
typeof 1; //=> "number"
typeof false; //=> "boolean"
typeof 's'; //=> "string"
typeof null; //=> "object"
typeof []; //=> "object"
typeof /[A-z]/; //=> "object"
typeof (() => {}); //=> "function"
typeof (async () => {}); //=> "function"
typeof undefined; //=> "undefined"
typeof BigInt(123); //=> "bigint"
```
- typeof는 null, 배열, 정규표현식는 특별한 구분없이 object로, 비동기 함수에 대해 function으로 표기한다.

## References
- https://ramdajs.com/docs/#type
