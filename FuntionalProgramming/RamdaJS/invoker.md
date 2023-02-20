## invoker
> Turns a named method with a specified arity into a function that can be called directly supplied with arguments and a target object.
- 평가를 위해서 받을 수 있는 인자의 수와 호출할 수 있는 메소드의 이름으로 하나의 함수로 바꾼다. 이 함수는 인자의 수와 메소드 이름만을 가지고 있지만 대상 객체와 인자가 주어지면 대상 객체가 가지고 있는 미리 지정한 이름의 함수를 주어진 인자들을 할당하여 직접 호출할 수 있다.

> The returned function is curried and accepts arity + 1 parameters where the final parameter is the target object.
- 반환된 함수는 커링되어 있으며, 지정된 '인자의 수'(`arity`) + 1 개의 파라메터를 가진다. 인자를 +1개 가지는 이유는 마지막 인자로 대상 객체를 지정해야 하기 때문이다.

> See also construct.

## 설명
-　메소드명과 인자의 수를 지정한 `invoker` 함수를 만들면, 만들어진 `invoker`함수에 지정한 갯수의 인자와 대상 객체를 인자로 주어 대상 객체에서 설정한 메소드명에 해당하는 메소드를 주어진 인자를 넣어 실행할 수 있다.
-　첫 번째 인자로는 함수를 평가하기 위해 받아야 할 인자의 수를 지정한다.
-　두 번째 인자로는 대상 오브젝트에서 실행할 메소드의 명을 지정한다.
-　첫 번째 인자와 두 번째 인자가 할당되면 설정된 `invoker`함수가 반환된다. 이 함수는 커링되어 있기 때문에 인자를 여러번 나누어 받을 수 있다.
-　이 함수에 첫 번째 인자로 설정한 인자의 수에 해당하는 인자를 넣고 마지막 인자로 지정된 메소드명을 호출할 대상 객체를 지정하면 대상 객체가 가진 메소드명에 해당하는 메소드에 주어진 인자를 넣고 실행한 결과를 반환하게 된다.

## 표현
```
Number → String → (a → b → … → n → Object → *)
```
- `Number →` 첫 번째 인자로 평가를 위해 필요한 인자의 수를 정한다.
- `→ String →` 두 번째 인자로 오브젝트의 메소드명을 지정한다. 이 때 아직 오브젝트는 지정되지 않은 상태이며 오브젝트의 이름만 지정한다.
- 그러면 함수가 하나 반환된다. `→ (a → b → … → n → Object → *)` 이 함수는 호출할 메소드에 넣을 인자를 커링된 형식으로 받고 `a → b → … → n`, `→ Object →` 마지막으로 오브젝트를 하나 받아서, 주어진 오브젝트(`Object`)에서 지정한 메소드명(`String`)에 해당하는 메소드를 호출하며 호출할 때 인자(`a → b → … → n`)를 넣어준다.
- 오브젝트의 지정한 메소드가 실행되므로 반환되는 결과는 다양(`→ *`)하다.

## 예제
```
const sliceFrom = R.invoker(1, 'slice');
sliceFrom(6, 'abcdefghijklm'); //=> 'ghijklm'
```
- `R.invoker(1, 'slice')` 어떤 대상으로부터 `slice` 함수를 호출하는데 호출할 때 인자를 하나만 받아 평가되는 함수로 설정한다.
- `sliceFrom(6, 'abcdefghijklm')`를 보면 첫 번째 인자로 `invoker` 함수에서 설정한 하나의 인자 `6`을 받고, 대상 오브젝트 `'abcdefghijklm'`를 지정한다.
- 결과적으로 `'abcdefghijklm'.slice(6)`을 평가한 결과를 반환한다.

```
const sliceFrom6 = R.invoker(2, 'slice')(6);
sliceFrom6(8, 'abcdefghijklm'); //=> 'gh'
```
- `R.invoker(2, 'slice')(6)` 어떤 대상으로부터 `slice` 함수를 호출하는데 위와 달리 호출할 때 인자를 2개 받아 평가되는 함수로 설정한다. 먼저 인자를 하나 `(6)` 받아서 6번째 인덱스 부터의 결과를 취득하는 `slice` 함수인 `sliceFrom6`를 만든다.
- `sliceFrom6(8, 'abcdefghijklm');`를 보면, 먼저 `invoker`에서 인자를 2개 받도록 설정을 했는데 미리 `6`을 받은 함수 `sliceFrom6`를 호출하므로 2개 인자 중 하나를 받은 상태이다. 나머지 하나의 인자를 더 받아 평가를 하는 함수이다. 대상 오브젝트 `'abcdefghijklm'`가 가지고 있는 `slice` 함수의 첫 번째 인자가 `6`으로 세팅된 함수에 두 번째 인자를 `8`로 세팅하여 평가를 한 결과를 반환한다.
- 따라서 `'abcdefghijklm'.slice(6, 8)`를 평가한 결과를 반환한다.

```
const dog = {
  speak: async () => 'Woof!'
};
const speak = R.invoker(0, 'speak');
speak(dog).then(console.log) //~> 'Woof!'
```
- `dog`이라는 객체는 `speak`라는 멤버를 가지고 있고 이 멤버는 메소드이다.
- `R.invoker(0, 'speak')`는 대상 오브젝트에서 `'speak'`라는 멤버를 호출하는 함수이며, 인자 없이 호출하여 평가하겠다는 의미를 가지고 있다.
- `speak(dog)`는 `doc` 오브젝트에서 `speak`라는 함수를 가져다가 쓰고 반환된 결과가 `promise` 타입에 해당하므로 `then`을 사용하여 해당 값을 받는다. 이 때 `then`의 인자는 일반적으로 `r => console.log(r)`의 코드여야 하는데 `console.log`만 왔는데도 출력이 되었다. `r => console.log(r)` 또한 함수이고 `console.log` 또한 함수이므로 첫 번째 매개변수를 `promise`의 결과값으로 전달받으므로 동일하다는 것을 알 수 있다.

## Reference
- https://ramdajs.com/docs/#invoker
