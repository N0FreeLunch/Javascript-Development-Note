## set
> Returns the result of "setting" the portion of the given data structure focused by the given lens to the given value.

> See also view, over, lens, lensIndex, lensProp, lensPath.

### 설명
- view, over, set과 같은 함수에 대상에서 특정한 프로퍼티를 뽑아내기 위한 설정을 담은 lens 함수와 함께 사용되어, set 함수는 랜즈 함수에서 지정한 프로퍼티의 값을 생성하거나 변경하는 용도로 사용한다.

### 표현
```
Lens s a → a → s → s
Lens s a = Functor f => (a → f a) → s → f s
```

#### 
- `Lens s a →`: 첫 번째 인자는 랜즈를 받는다. 랜즈는 대상의 타입 파라메터를 s라고 했을 때 s의 프로퍼티 a를 뽑는 렌즈이다.
- `→ s →`: 두 번째 인자로는 랜즈를 적용할 대상을 받는다. 대상의 타입 파라메터는 s인데 첫 번째 인자로 받은 랜즈에서 프로퍼티를 뽑을 수 있는 대상인 s와 동일한 타입이 되어야 한다.
- `→ s`: 최종 결과는 랜즈가 받는 타입 파라메터 s를 반환한다. 이 타입 파라메터 s는 랜즈로 a 타입의 프로퍼티를 뽑아낼 수 있는 대상이다.

####
- `a = Functor f =>`: 

### 예제
```js
const xLens = R.lensProp('x');

R.set(xLens, 4, {x: 1, y: 2});  //=> {x: 4, y: 2}
R.set(xLens, 8, {x: 1, y: 2});  //=> {x: 8, y: 2}
```
- 오브젝트에서 지정한 프로퍼티의 값을 꺼내기 위한 lens 함수를 만드는 `R.lensProp` 함수를 

## Referece
- https://ramdajs.com/docs/#set
