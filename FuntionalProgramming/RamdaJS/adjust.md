## adjust
`R.adjust(indexNumber, callbackFunction, list)`
- indexNumber : 콜백함수를 적용할 리스트의 인덱스 번호, 음수 인덱스도 사용 가능하다.

## 설명
- 지정한 인덱스의 원소에 정의한 콜백 함수를 적용시킨 후 리스트를 반환한다.
- 리스트의 특정한 원소를 지정해서 해당 원소를 변화 시키고자 할 때 사용한다.
- 여러 원소를 변경시키는 것이 아니라 단일 원소를 변경시킨다는 문제점이 있다.

## 예시
```
R.adjust(1, R.toUpper, ['a', 'b', 'c', 'd']);      //=> ['a', 'B', 'c', 'd']
R.adjust(-1, R.toUpper, ['a', 'b', 'c', 'd']);     //=> ['a', 'b', 'c', 'D']
```

## Reference
- https://ramdajs.com/docs/#adjust
