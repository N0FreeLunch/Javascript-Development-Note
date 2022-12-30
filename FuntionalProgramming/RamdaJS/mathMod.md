## mathMod
> mathMod behaves like the modulo operator should mathematically, unlike the % operator (and by extension, R.modulo). So while -17 % 5 is -2, mathMod(-17, 5) is 3. mathMod requires Integer arguments, and returns NaN when the modulus is zero or negative.

> See also modulo.

## 설명
- 모듈러 연산을 하는 함수이다. 
- 모듈러 연산은 0 또는 양의 정수를 남기는 연산이다.
- 정수 범위의 나눗셈 `a/b`에 대해 a는 피젯수, b는 제수로 부르며 `(피젯수) - (제수의 배수)`가 최소가 되는 0 또는 양의 정수 값이다.
- 예를 들어 17/5이면 17에서 15(5의 3배수)를 뺀 값으로 나머지는 2이다. 음수의 경우 -17/5이면 -17에서 -15(5의 -3배수)를 빼면 나머지는 -2가 되므로 0 또는 양의 정수가 아니다. 따라서 -17에서 -20(5의 -4배수)을 뺀 값으로 나머지는 3으로 0 또는 양의 정수에 해당한다.

## 표현
```
Number → Number → Number
```
- `Number →` 첫 번째 인자로 빼기를 당할 대상인 피젯수를 받는다.
- `→ Number →` 두 번째 인자로 뺄 대상인 제수를 받는다.
- `→ Number` 제수를 반복적으로 빼어 더 이상 뺄 수 없을 만큼 뺀 나머지 값을 반환한다.

## 예제
```
R.mathMod(-17, 5);  //=> 3
R.mathMod(17, 5);   //=> 2
R.mathMod(17, -5);  //=> NaN
R.mathMod(17, 0);   //=> NaN
R.mathMod(17.2, 5); //=> NaN
R.mathMod(17, 5.3); //=> NaN
```
- `R.mathMod(-17, 5)`는 `-17 - 20`이므로 3이다.
- `R.mathMod(17, 5)`는 `17 - 5`이므로 2이다.
- `R.mathMod(17, -5)` 제수가 음수가 될 수 없으므로 NaN을 반환한다.
- `R.mathMod(17, 0)` 제수가 0이 될 수 없으므로 NaN을 반환한다.

```
const clock = R.mathMod(R.__, 12);
clock(15); //=> 3
clock(24); //=> 0
```

```
const seventeenMod = R.mathMod(17);
seventeenMod(3);  //=> 2
seventeenMod(4);  //=> 1
seventeenMod(10); //=> 7
```

## Reference
- https://ramdajs.com/docs/#mathMod
