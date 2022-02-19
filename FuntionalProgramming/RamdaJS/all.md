## all
`R.all(predicate, list)`
- predicate는 술어 함수를 의미하며, 대상의 참 거짓을 판별할 때 사용한다. predicate 부분에는 리스트 원소의 참 거짓을 판별할 수 있는 콜백함수를 정의한다.

## 설명
- 술어 함수와 리스트를 인자로 받아서, 리스트 내의 모든 원소가 주어진 술어 함수를 만족하는지 확인하고 모든 함수가 주어진 술어 함수를 만족하면 true, 주어진 술어 함수를 만족하지 않으면 false를 반환한다. 

## 예시
```
const equals3 = R.equals(3);
R.all(equals3)([3, 3, 3, 3]); //=> true
R.all(equals3)([3, 3, 1, 3]); //=> false
```

## Reference
- https://ramdajs.com/docs/#all
