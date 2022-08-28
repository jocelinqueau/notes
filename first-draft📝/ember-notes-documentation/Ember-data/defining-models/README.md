# Defining Models

A model is a class that defines the properties and behavior of the data that you present to the user. Anything that the user expects to see if they leave your app and come back later (or if they refresh the page) should be represented by a model.

## -

When you want a new model for your application you need to create a new file under the models folder and extend from DS.Model. This is more conveniently done by using one of Ember CLI's generator commands. For instance, let's create a person model

`ember generate model person`

> Ember Data models are normally setup using the singular form (which is why we use `person` instead of `people` here)

## Defining Attributes

```js
import DS from 'ember-data';

export default DS.Model.extend({
  firstName: DS.attr(),
  lastName: DS.attr(),
  birthday: DS.attr()
});
```

You can use attributes like any other property, including as part of a computed property. Frequently, you will want to define computed properties that combine or transform primitive attributes.

```js
import DS from 'ember-data';
import { computed } from '@ember/object';

export default DS.Model.extend({
  firstName: DS.attr(),
  lastName: DS.attr(),

  fullName: computed('firstName', 'lastName', function() {
    return `${this.firstName} ${this.lastName}`;
  })
});
```

## Transforms

You may find the type of an attribute returned by the server does not match the type you would like to use in your JavaScript code. Ember Data allows you to define simple serialization and deserialization methods for attribute types called transforms. You can specify that you would like a transform to run for an attribute by providing the transform name as the first argument to the DS.attr method. Ember Data supports attribute types of string, number, boolean, and date, which coerce the value to the JavaScript type that matches its name.

Transforms are not required. If you do not specify a transform name Ember Data will do no additional processing of the value.


```js
import DS from 'ember-data';

export default DS.Model.extend({
  name: DS.attr('string'),
  age: DS.attr('number'),
  admin: DS.attr('boolean'),
  birthday: DS.attr('date')
});
```

## Custom Transforms

You can also create custom transforms with Ember CLI's transform generator:

`ember generate transform dollars`

```js
import DS from 'ember-data';

export default DS.Transform.extend({
  deserialize(serialized) {
    return serialized / 100; // returns dollars
  },

  serialize(deserialized) {
    return deserialized * 100; // returns cents
  }
});
```

A transform has two functions: serialize and deserialize. Deserialization converts a value to a format that the client expects. Serialization does the reverse and converts a value to the format expected by the persistence layer.

You would use the custom dollars transform like this:

```js
import DS from 'ember-data';

export default DS.Model.extend({
  spent: DS.attr('dollars')
});
```

DS.attr can use options

At the moment the only option available is defaultValue, which can use a value or a function to set the default value of the attribute if one is not supplied.

In the following example we define that verified has a default value of false and createdAt defaults to the current date at the time of the model's creation:

```js
import DS from 'ember-data';

export default DS.Model.extend({
  username: DS.attr('string'),
  email: DS.attr('string'),
  verified: DS.attr('boolean', { defaultValue: false }),
  createdAt: DS.attr('date', {
    defaultValue() { return new Date(); }
  })
});
```

## Read-only Attributes

When the API returns a deeply nested, read-only object or array, there is no need to create multiple models with DS.attr('hasMany') or DS.attr('belongsTo') relationships. This could result in a potentially large amount of unnecessary code. You can access these objects in the template without transforming them. This can be done with DS.attr() (No attribute type).

The following example shows how to define these attributes without transforming them and accessing them within a template:

```js
location: DS.attr() // a read-only object
tags: DS.attr() // a read-only array
```

```hbs
{{this.model.location.latitude}}
```