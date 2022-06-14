## tap
- R.tap()
> Runs the given function with the supplied object, then returns the object.
- `R.tap` 함수는 인자로 받는 함수와 이 함수의 인자로 넣을 대상을 인자로 받고, 인자로 받는 함수의 인자로 받을 대상을 `R.tap()`의 반환 값으로 한다.
> Acts as a transducer if a transformer is given as second parameter.
- 변환기(transducer)로서 행동한다. 변환기는 두 번째 인자로 받은 것을 그대로 반환한다.
- 여기서 오브젝트는 오브젝트 타입이 아닌 '대상'을 의미하며 모든 타입이 가능하다.

## 설명
- `R.tap(function, object)`
- 첫 번째 인자로 함수를 받고, 두 번째 인자로 반환되는 대상을 넣는다. 두 번째 인자는 첫 번째 인자의 함수에 넣을 인자로 공급된다.
- `R.tap(function, object)` 함수의 반환 값은 두 번째 인자에 넣은 대상이며 첫 번째 인자의 함수는 순수 함수의 특성을 유지하면서 사이드이펙트를 만들기 위해 사용한다.
- 어떤 값을 사용할 때 이 값을 통해 부수적으로 실행이 되는 사이드 이펙트를 정의하기 위해 사용한다.

## 표현
```
(a → *) → a → a
```
- `(a → *)` a는 어떠한 대상도 가능한 all을 의미. 첫 번째 인자로는 임의의 타입 a를 단일 인자로 받는 함수를 인자로 받는다.
- `→ a →` 두 번째 인자로는 대상 값을 의미
- `→ a` 반환 되는 값은 두 번째 인자의 대상이 반환 됨

## 예제
```
const sayX = x => console.log('x is ' + x);
R.tap(sayX, 100); //=> 100
// logs 'x is 100'
```
- `sayX`는 `x => console.log('x is ' + x)`라는 함수
- `R.tap`의 첫 번째 인자로 사이드 이펙트로 실행할 함수를 할당하고, 두 번째 인자로 `100`이란 값을 할당
- `R.tap(sayX, 100);`이 실행되면서 100이란 값이 `sayX` 함수의 인자로 할당이 되고 `R.tap(sayX, 100);`의 결과 값이 100이 된다.
- `sayX`에 100이란 값을 인자로 넣어 사이드 이펙트를 실행하다.


## Reference
- https://ramdajs.com/docs/#tap
