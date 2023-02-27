## clone
> Creates a deep copy of the source that can be used in place of the source object without retaining any references to it. 
> The source object may contain (nested) Arrays and Objects, Numbers, Strings, Booleans and Dates. Functions are assigned by reference rather than copied.
> Dispatches to a clone method if present.
> Note that if the source object has multiple nodes that share a reference, the returned object will have the same structure, but the references will be pointed to the location within the cloned value.

## 표현
```
{*} → {*}
```

## 예제
```
const objects = [{}, {}, {}];
const objectsClone = R.clone(objects);
objects === objectsClone; //=> false
objects[0] === objectsClone[0]; //=> false
```

## Reference
- https://ramdajs.com/docs/#clone
