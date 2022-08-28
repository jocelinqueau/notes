# anchors

The caret `^` and dollar `$` characters have special meaning in a regexp. They are called “anchors”.

The caret `^` matches at the beginning of the text, and the dollar `$` – at the end.

For instance, let’s test if the text starts with `Mary`:

```js
let str1 = "Mary had a little lamb";
alert( /^Mary/.test(str1) ); // true
```

The pattern `^Mary` means: “string start and then Mary”.

Similar to this, we can test if the string ends with `snow` using `snow$`:

[](https://javascript.info/regexp-anchors# "run")

[](https://javascript.info/regexp-anchors# "open in sandbox")

```js
let str1 = "its fleece was white as snow";
alert( /snow$/.test(str1) ); // true
```

In these particular cases we could use string methods `startsWith/endsWith` instead. Regular expressions should be used for more complex tests.


Anchors behave differently if flag m is present. We’ll see that in the next article.

Anchors have “zero width”

Anchors `^` and `$` are tests. They have zero width.

In other words, they do not match a character, but rather force the regexp engine to check the condition (text start/end).