## subtract
> Subtracts its second argument from its first argument.
> 첫 번째 인자에서 두 번째 인자를 뺀다.

> See also add.

### 설명
- '첫번째 인자' - '두 번째 인자', 뺄셈을 하기 위해 두 인자는 Number 타입의 값을 받아야 한다.

### 표현
```
Number → Number → Number
```
- `Number →`: 첫 번째 인자로 값을 빼기 위한 대상을 지정한다.
- `→ Number →`: 두 번째 인자로 뺄 값을 지정한다.
- `→ Number`: 첫 번째 인자에서 두 번째 인자르 뺀 결과를 반환한다.

### 예제
```js
R.subtract(10, 8); //=> 2

const minus5 = R.subtract(R.__, 5);
minus5(17); //=> 12

const complementaryAngle = R.subtract(90);
complementaryAngle(30); //=> 60
complementaryAngle(72); //=> 18
```
- `R.subtract(10, 8)`는 10 - 8 이므로 2이다.
- `R.subtract(R.__, 5)`는 첫 번째 인자를 나중에 받아 평가하도록 `R.__`를 인자로 전달하였다. `minus5`는 `R.subtract(R.__, 5)`가 첫번째 인자를 못 받았기 때문에 인자로 받은 값에서 5를 빼는 함수가 된다.
- `R.subtract(90)`는 두 선이 만나는 사잇각을 받아서 그 여각을 구하는 `complementaryAngle`라는 이름을 부여하였다. 사잇각이 30이라면 `complementaryAngle(30)`에 의해 여각은 60이고, 사잇각이 72라면 `complementaryAngle(72)`에 의해 여각이 18이 된다.

## Reference
- https://ramdajs.com/docs/#subtract
