## promap
> Takes two functions as pre- and post- processors respectively for a third function, i.e. promap(f, g, h)(x) === g(h(f(x))).
- 세 번째 함수에 대해 pre- 와 post- 처리기(processor) 역할을 하는 두 개의 함수를 받는다.
- 함수 f는 preprocessor에 해당하며, g는 postprocessor에 해당한다. 세 번째로 받은 함수는 변환의 핵심이 되는 함수 h에 해당한다. 즉, `promap(f, g, h)(x) === g(h(f(x))).`이다.

> Dispatches to the promap method of the third argument, if present, according to the FantasyLand Profunctor spec.
- [FantasyLand의 Profunctor 스펙](https://github.com/fantasyland/fantasy-land?tab=readme-ov-file#profunctor)에 따라 세 번째 인자가 존재하면, promap 메소드는 실행(dispatche)된다.

> Acts as a transducer if a transformer is given in profunctor position.

> See also transduce.

### 설명

### 표현
```
(a → b) → (c → d) → (b → c) → (a → d)
Profunctor p => (a → b) → (c → d) → p b c → p a d
```

### 예제
```js
const decodeChar = R.promap(s => s.charCodeAt(), String.fromCharCode, R.add(-8))
const decodeString = R.promap(R.split(''), R.join(''), R.map(decodeChar))
decodeString("ziuli") //=> "ramda"
```

## Reference
- https://ramdajs.com/docs/#promap
