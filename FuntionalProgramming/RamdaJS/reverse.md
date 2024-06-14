## reverse
> Returns a new list or string with the elements or characters in reverse order.
- 원소의 순서가 역전된 리스트나 문자의 순서가 역전된 문자열을 새 것으로 반환한다.

### 설명
- 문자열의 각 문자의 순서를 거꾸로 한 문자열 또는 배열의 원소의 순을 거꾸로 나열한 배열을 얻는다.
- 받을 수 있는 인자의 종류는 두 가지이며, 유사한 처리를 하지만 배열에 대한 처리와 문자열에 대한 처리를 하므로 동일한 처리를 하는 것은 아니다. 사실상 2개의 함수의 기능을 갖고 있지만, 두 가지 기능을 인자의 종류에 따라 달리 처리하는 하나의 함수로 보면된다.

### 표현
```
[a] → [a]
String → String
```

#### 배열
- `[a] →`: 첫 번째 인자로 배열을 받아서
- `→ [a]`: 원소의 순서가 역전된 배열을 반환한다.

#### 문자열
- `String →`: 첫 번째 인자로 문자열을 받아서
- `→ String`: 문자의 순서가 역전된 문자열을 반환한다.

### 예제
```
R.reverse([1, 2, 3]);  //=> [3, 2, 1]
R.reverse([1, 2]);     //=> [2, 1]
R.reverse([1]);        //=> [1]
R.reverse([]);         //=> []

R.reverse('abc');      //=> 'cba'
R.reverse('ab');       //=> 'ba'
R.reverse('a');        //=> 'a'
R.reverse('');         //=> ''
```
- 예제를 보는 것만으로 명확하므로 설명이 필요하지 않다.

## Reference
- https://ramdajs.com/docs/#reverse
