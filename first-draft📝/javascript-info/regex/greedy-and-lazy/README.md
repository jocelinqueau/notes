# -

## Greedy search

TL;DR 

```js
let regexp = /".+"/g;

let str = 'a "witch" and her "broom" is one';

alert( str.match(regexp) ); // "witch" and her "broom"
```

so regex try to find the first match, then when it find it, it complete the second pattern, `.+` which match all the rest of the string, then it try to match the last pattern, so it goes back and try to find a match, then when find return the string

that's greedy search

 If the regular expression has flag g, then the search will continue from where the first match ends. There are no more quotes in the rest of the string is one, so no more results.

 In the greedy mode (by default) a quantified character is repeated as many times as possible.

The regexp engine adds to the match as many characters as it can for .+, and then shortens that one by one, if the rest of the pattern doesn’t match.

For our task we want another thing. That’s where a lazy mode can help.

## Lazy mode

The lazy mode of quantifiers is an opposite to the greedy mode. It means: “repeat minimal number of times”.

We can enable it by putting a question mark '?' after the quantifier, so that it becomes *? or +? or even ?? for '?'.

The regexp /".+?"/g works as intended: it finds "witch" and "broom":

```js
let regexp = /".+?"/g;

let str = 'a "witch" and her "broom" is one';

alert( str.match(regexp) ); // "witch", "broom"
```

## Laziness is only enabled for the quantifier with ?.

## Alternative approach