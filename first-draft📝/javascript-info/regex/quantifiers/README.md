# Quantifiers +, *, ? and {n}

## Quantity {n}

```js
alert( "I'm not 12, but 1234 years old".match(/\d{3,5}/) ); // "1234"
```

```js
alert( "I'm not 12, but 345678 years old".match(/\d{3,}/) ); // "345678"
```

## Shorthands

\+ means “one or more”, the same as {1,}.

\?
Means “zero or one”, the same as {0,1}. In other words, it makes the symbol optional.

For instance, the pattern ou?r looks for o followed by zero or one u, and then r.

So, colou?r finds both color and colour


\* Means “zero or more”, the same as {0,}.