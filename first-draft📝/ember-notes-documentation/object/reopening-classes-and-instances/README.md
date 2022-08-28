# Reopening Classes and Instances

You don't need to define a class all at once. You can reopen a class and define new properties using the [`reopen()`](https://api.emberjs.com/ember/3.12/functions/@ember%2Fobject/reopen) method.

```js
Person.reopen({
  // override `say` to add an ! at the end
  say(thing) {
    this._super(thing + '!');
  }
});
```

`reopen()` is used to add instance methods and properties that are shared across all instances of a class. It does not add methods and properties to a particular instance of a class as in vanilla JavaScript (without using prototype).

But when you need to add static methods or static properties to the class itself you can use [`reopenClass()`](https://api.emberjs.com/ember/3.12/functions/@ember%2Fobject/reopenClass).
