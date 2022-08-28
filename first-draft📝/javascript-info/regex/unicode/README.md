# Unicode

## [Summary](https://javascript.info/regexp-unicode#summary)

Flag `u` enables the support of Unicode in regular expressions.

That means two things:

1.  Characters of 4 bytes are handled correctly: as a single character, not two 2-byte characters.
2.  Unicode properties can be used in the search: `\p{…}`.

With Unicode properties we can look for words in given languages, special characters (quotes, currencies) and so on.


## -

JavaScript uses Unicode encoding for strings. Most characters are encoded with 2 bytes, but that allows to represent at most 65536 characters.

That range is not big enough to encode all possible characters, that’s why some rare characters are encoded with 4 bytes, for instance like 𝒳 (mathematical X) or 😄 (a smile), some hieroglyphs and so on.

So characters like a and ≈ occupy 2 bytes, while codes for 𝒳, 𝒴 and 😄 are longer, they have 4 bytes.

Long time ago, when JavaScript language was created, Unicode encoding was simpler: there were no 4-byte characters. So, some language features still handle them incorrectly.

For instance, length thinks that here are two characters:

```js
alert('😄'.length); // 2
alert('𝒳'.length); // 2
```

Unlike strings, regular expressions have flag u that fixes such problems. With such flag, a regexp handles 4-byte characters correctly. And also Unicode property search becomes available, we’ll get to it next.

## Unicode properties \p{…}

Every character in Unicode has a lot of properties. They describe what “category” the character belongs to, contain miscellaneous information about it.

For instance, if a character has Letter property, it means that the character belongs to an alphabet (of any language). And Number property means that it’s a digit: maybe Arabic or Chinese, and so on.

We can search for characters with a property, written as \p{…}. To use \p{…}, a regular expression must have flag u.

For instance, \p{Letter} denotes a letter in any language. We can also use \p{L}, as L is an alias of Letter. There are shorter aliases for almost every property.

In the example below three kinds of letters will be found: English, Georgian and Korean.

```js
let str = "A ბ ㄱ";

alert( str.match(/\p{L}/gu) ); // A,ბ,ㄱ
alert( str.match(/\p{L}/g) ); // null (no matches, \p doesn't work without the flag "u")
```

Here’s the main character categories and their subcategories:
​

- Letter `L`:
  - lowercase `Ll`
  - modifier `Lm`,
  - titlecase `Lt`,
  - uppercase `Lu`,
  - other `Lo`.
- Number `N`:
  - decimal digit `Nd`,
  - letter number `Nl`,
  - other `No`.
- Punctuation `P`:
  - connector `Pc`,
  - dash `Pd`,
  - initial quote `Pi`,
  - final quote `Pf`,
  - open `Ps`,
  - close `Pe`,
  - other `Po`.
- Mark `M` (accents etc):
  - spacing combining `Mc`,
  - enclosing `Me`,
  - non-spacing `Mn`.
- Symbol `S`:
  - currency `Sc`,
  - modifier `Sk`,
  - math `Sm`,
  - other `So`.
- Separator `Z`:
  - line `Zl`,
  - paragraph `Zp`,
  - space `Zs`.
- Other `C`:
  - control `Cc`,
  - format `Cf`,
  - not assigned `Cn`,
  - private use `Co`,
  - surrogate `Cs`.


### [Example: currency](https://javascript.info/regexp-unicode#example-currency)

Characters that denote a currency, such as `$`, `€`, `¥`, have Unicode property `\p{Currency_Symbol}`, the short alias: `\p{Sc}`.

Let’s use it to look for prices in the format “currency, followed by a digit”:

[](https://javascript.info/regexp-unicode# "run")

[](https://javascript.info/regexp-unicode# "open in sandbox")

```
let regexp = /\p{Sc}\d/gu;

let  str = `Prices: $2, €1, ¥9`;

alert( str.match(regexp) ); // $2,€1,¥9
```

## [Summary](https://javascript.info/regexp-unicode#summary)

Flag `u` enables the support of Unicode in regular expressions.

That means two things:

1.  Characters of 4 bytes are handled correctly: as a single character, not two 2-byte characters.
2.  Unicode properties can be used in the search: `\p{…}`.

With Unicode properties we can look for words in given languages, special characters (quotes, currencies) and so on.

