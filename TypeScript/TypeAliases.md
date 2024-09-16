## 타입 별칭

### 복합타입

타입은 '변수: 타입'의 방식으로 변수에 타입을 지정할 수 있다.

```ts
const f = (a: string | number) => {
}
```

여러 타입을 복합적으로 사용하는 경우, 복합 타입에 명칭을 부여할 수 있다.

```ts
type A = string | number;

const f = (a: A) => {
}
```

### 구조를 포함한 타입
```ts
const f = (person: {name: string, age: number, gender: 'M'|'F'}) => {
}
```

```ts
type Person = {name: string, age: number, gender: 'M'|'F'};

const f = (person: Person) => {
}
```
