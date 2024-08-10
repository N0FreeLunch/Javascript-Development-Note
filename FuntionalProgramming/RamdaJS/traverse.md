## traverse
> Maps an Applicative-returning function over a Traversable, then uses sequence to transform the resulting Traversable of Applicative into an Applicative of Traversable.

> Dispatches to the traverse method of the third argument, if present.

> See also sequence.

### 설명

### 표현
```
fantasy-land/of :: TypeRep f => f ~> a → f a
(Applicative f, Traversable t) => TypeRep f → (a → f b) → t a → f (t b)
(Applicative f, Traversable t) => (b → f b) → (a → f b) → t a → f (t b)
```

### References
```js
// Returns `Maybe.Nothing` if the given divisor is `0`
const safeDiv = n => d => d === 0 ? Maybe.Nothing() : Maybe.Just(n / d)

R.traverse(Maybe.of, safeDiv(10), [2, 4, 5]); //=> Maybe.Just([5, 2.5, 2])
R.traverse(Maybe.of, safeDiv(10), [2, 0, 5]); //=> Maybe.Nothing

// Using a Type Representative
R.traverse(Maybe, safeDiv(10), Right(4)); //=> Just(Right(2.5))
R.traverse(Maybe, safeDiv(10), Right(0)); //=> Nothing
R.traverse(Maybe, safeDiv(10), Left("X")); //=> Just(Left("X"))
```

## Reference
- https://ramdajs.com/docs/#traverse
