# The IO monad in Javascript — How does it compare to other techniques?


[link](https://medium.com/@magnusjt/the-io-monad-in-javascript-how-does-it-compare-to-other-techniques-124ef8a35b63)
In short, a monad is anything that can be mapped and flatMapped (though map can always be derived in terms of flatMap, so is not as important)

map is a function that takes a function `(val: T) => T`, and returns a new monad (of the same type as what you called map on).
In other words, map lets you change the thing that lives inside the monad.

flatMap is a function that takes a function `(val: T) => Monad<T>`, and returns a new monad (of the same type as what you called flatMap on).
So flatMap is just a map followed by a flat, where flat unpacks the monad you returned.

## Examples

An array is (almost) a monad:

```ts
[1, 2, 3].map(x => x * 2) // [2, 4, 6]
[1, 2, 3].flatMap(x => [x, 10]) // [1, 10, 2, 10, 3, 10]
```

It’s “almost” a monad because map and flatMap supports more than one argument, but that’s not important right now.

Another example that is (almost) a monad is a promise:

```ts
// map
Promise.resolve(5).then(x => x * 2) // Promise of 10//

// flatMap

Promise.resolve(5).then(x => Promise.resolve(x * 2)) // Promise of 10
```

It’s “almost” a monad because

flatMap is called “then”
“then” also does the job of map
“then” can take more than one argument