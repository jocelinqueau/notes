# -

## --

### Introducing: Ember Objects[](https://guides.emberjs.com/v3.12.0/object-model/#toc_introducing-ember-objects)

The [Ember Object](https://api.emberjs.com/ember/3.12/classes/EmberObject) class extends plain JavaScript objects to provide core framework functions such as participating in Ember's [binding system](https://guides.emberjs.com/v3.12.0/object-model/bindings/) or how changes to an object automatically trigger updates to the user interface.

Most objects in Ember, including Routes, Models, Services, Mixins, Controllers, and Components extend the `EmberObject` class.

### More on Ember Objects[](https://guides.emberjs.com/v3.12.0/object-model/#toc_more-on-ember-objects)

The [@ember/object](https://api.emberjs.com/ember/3.12/modules/@ember%2Fobject) package also provides a class system, supporting features like mixins and constructor methods, and being observable.

Some features in Ember's object model are not present in JavaScript classes or common patterns, but all are aligned as much as possible with the language and proposed additions.

Ember also extends the JavaScript `Array` prototype with its [@ember/enumerable](https://api.emberjs.com/ember/3.12/classes/Enumerable) interface to provide change observation for arrays.

Finally, Ember extends the `String` prototype with a few [formatting and localization methods](https://api.emberjs.com/ember/3.12/classes/String).
