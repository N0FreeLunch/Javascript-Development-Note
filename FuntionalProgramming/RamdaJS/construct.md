## construct
> Wraps a constructor function inside a curried function that can be called with the same arguments and returns the same type.

> See also invoker.

## 설명


## 표현
```
(* → {*}) → (* → {*})
```

## 예제
```
// Constructor function
function Animal(kind) {
  this.kind = kind;
};
Animal.prototype.sighting = function() {
  return "It's a " + this.kind + "!";
}

const AnimalConstructor = R.construct(Animal)

// Notice we no longer need the 'new' keyword:
AnimalConstructor('Pig'); //=> {"kind": "Pig", "sighting": function (){...}};

const animalTypes = ["Lion", "Tiger", "Bear"];
const animalSighting = R.invoker(0, 'sighting');
const sightNewAnimal = R.compose(animalSighting, AnimalConstructor);
R.map(sightNewAnimal, animalTypes); //=> ["It's a Lion!", "It's a Tiger!", "It's a Bear!"]
```

#### Animal 객체의 생성자 만들기
```
function Animal(kind) {
  this.kind = kind;
};
```

#### Animal 객체의 메소드 추가하기
```
Animal.prototype.sighting = function() {
  return "It's a " + this.kind + "!";
}
```

#### Animal 객체에 R.construct 함수 사용하기
```
const AnimalConstructor = R.construct(Animal)
```
```
AnimalConstructor('Pig')
```
- `construct` 함수에 객체 `Animal`을 인자로 넣어 반환된 함수(`AnimalConstructor`)에 인자를 넣으면 받은 인자와 동일한 인자가 생성자에 할당된 객체를 반환한다 따라서 `{"kind": "Pig", "sighting": function (){...}};` 생성자로 `"kind"`에 `"Pig"`가 할당된 값의 객체가 반환된다.


## Reference
- https://ramdajs.com/docs/#construct
