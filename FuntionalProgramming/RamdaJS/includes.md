## includes
> Returns true if the specified value is equal, in R.equals terms, to at least one element of the given list; false otherwise. Also works with strings.
- 주어진 리스트의 적어도 하나의 원소가 지정된 값과 `R.equals` 함수를 통해 평가 되었을 때 같다면 참을 아니면 거짓을 반환한다. 리스트 뿐만 아니라 문자열에도 적용된다. 

## 표현
```
a → [a] → Boolean
```
- `a →` 첫 번째 인자로 어떤 값을 지정한다.
- `→ [a] →` 두 번째 인자로 배열을 지정한다. 
- `→ Boolean` 만약 두 번째 인자의 배열의 원소에서 첫 번째 인자와 일치하는 값이 존재하면 참을 아니면 거짓을 반환한다.

## 설명
- 주어진 배열에서 특정 원소가 존재하는지 확인한다. 존재하면 참을 아니면 거짓을 반환한다.
- 배열에 대해서는 배열의 원소 하나와 매칭이 되는지 확인하지만, 문자열의 경우에는 첫 번째 인자로 한 문자의 문자열이든 두 문자의 문자열이든 문자의 길이에 관계 없이 존재하는지 확인할 수 있다.

## 예제
```
R.includes(3, [1, 2, 3]); //=> true
R.includes(4, [1, 2, 3]); //=> false
R.includes({ name: 'Fred' }, [{ name: 'Fred' }]); //=> true
R.includes([42], [[42]]); //=> true
R.includes('ba', 'banana'); //=>true
```

## Reference
- https://ramdajs.com/docs/#includes
