# Bindings | linking ( 2way and 1 way)

> Note: Unlike most other frameworks that include some sort of binding implementation, bindings in Ember.js can be used with any object. That said, bindings are most often used within the Ember framework itself, and for most problems Ember app developers face, computed properties are the appropriate solution.

The easiest way to create a two-way binding is to use a [`computed.alias()`](https://api.emberjs.com/ember/3.12/classes/@ember%2Fobject%2Fcomputed/methods/alias?anchor=alias), that specifies the path to another object.

```js
import EmberObject from '@ember/object';
import { alias } from '@ember/object/computed';

husband = EmberObject.create({
  pets: 0
});

Wife = EmberObject.extend({
  pets: alias('husband.pets')
});

wife = Wife.create({
  husband: husband
});

wife.get('pets'); // 0

// Someone gets a pet.
husband.set('pets', 1);
wife.get('pets'); // 1
```

## One-Way Bindings

```js
import EmberObject, { computed } from '@ember/object';
import Component from '@ember/component';
import { oneWay } from '@ember/object/computed';

user = EmberObject.create({
  fullName: 'Kara Gates'
});

UserComponent = Component.extend({
  userName: oneWay('user.fullName')
});

userComponent = UserComponent.create({
  user: user
});

// Changing the name of the user object changes
// the value on the view.
user.set('fullName', 'Krang Gates');
// userComponent.userName will become "Krang Gates"

// ...but changes to the view don't make it back to
// the object.
userComponent.set('userName', 'Truckasaurus Gates');
user.get('fullName'); // "Krang Gates"
```
