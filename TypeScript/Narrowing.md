## type narrowing (타입 좁히기)

변수의 타입으로 여러 타입이 지정된 경우 일부 타입의 케이스에서만 사용하도록 코드를 작성할 수 있다.

```ts
const f = (a: number | string) => {
  if (typeof a === "string") {
    console.log("'a' is always treated as a string in this block.");
  } else {
    console.log("'a' is always treated as a number in this block.");
  }
};
```

타입스크립트에서 특정 타입만 사용되는 블록을 만들고 싶다면 타입에 따른 조건 분기 코드를 만들면 된다. `if (typeof a === "string")`에 의해 분기된 블록 내에서는 항상 a는 문자열로 다뤄지기 때문에 문자열 변수를 가정한 코드를 짰을 때 아무런 문제가 없으며, 수 변수를 가정한 코드를 짜면 타입 에러가 발생한다. 이에 반해 뒤 따르는 `else` 문에 의해 분기되는 블록은 a가 number 또는 string 타입이기 때문에 수 변수를 가정한 코드를 짰을 때 아무런 문제가 없으며, 문자열 변수를 가정한 코드를 짜면 타입 에러가 발생한다.

