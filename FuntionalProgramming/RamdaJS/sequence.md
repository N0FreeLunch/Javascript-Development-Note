## sequence
> Transforms a Traversable of Applicative into an Applicative of Traversable.

> Dispatches to the "fantasy-land/traverse" or the traverse method of the second argument, if present.

> See also traverse.

### 표현
```
fantasy-land/of :: TypeRep f => f ~> a → f a
(Applicative f, Traversable t) => TypeRep f → t (f a) → f (t a)
(Applicative f, Traversable t) => (a → f a) → t (f a) → f (t a)
```

### 예제
```js
R.sequence(Maybe.of, [Just(1), Just(2), Just(3)]);   //=> Just([1, 2, 3])
R.sequence(Maybe.of, [Just(1), Just(2), Nothing()]); //=> Nothing()

R.sequence(R.of(Array), Just([1, 2, 3])); //=> [Just(1), Just(2), Just(3)]
R.sequence(R.of(Array), Nothing());       //=> [Nothing()]
```

### Reference
- https://ramdajs.com/docs/#sequence
