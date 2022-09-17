## dropLast
> Returns a list containing all but the last n elements of the given list.
> Acts as a transducer if a transformer is given in list position.

## 표현
```
Number → [a] → [a]
Number → String → String
```

## 설명
- drop이 앞에서 부터 지정한 번째까지의 원소를 지운 것에 반해 dropLast는 뒤에서 부터 지정한 번째까지의 원소를 지운다.

## 예제
```
R.dropLast(1, ['foo', 'bar', 'baz']); //=> ['foo', 'bar']
R.dropLast(2, ['foo', 'bar', 'baz']); //=> ['foo']
R.dropLast(3, ['foo', 'bar', 'baz']); //=> []
R.dropLast(4, ['foo', 'bar', 'baz']); //=> []
R.dropLast(3, 'ramda');               //=> 'ra'
```

## Reference
- https://ramdajs.com/docs/#dropLast
