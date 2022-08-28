# Defining Models

When you want a new model for your application you need to create a new file under the models folder and extend from `Model` as cli: `ember generate model person`

```js
import Model from '@ember-data/model';

export default class PersonModel extends Model {
}
```

>Zoey says...
Ember Data models are normally setup using the singular form (which is why we use `person` instead of `people` here) | *just like rails*

## Defining Attributes

The person model we generated earlier didn't have any attributes. Let's add some

```js
import Model, { attr } from '@ember-data/model';

export default class PersonModel extends Model {
  @attr title;
  @attr name;
  @attr birthday;
}
```

You can use attributes like any other property, including from within getter functions.

```js
import Model, { attr } from '@ember-data/model';

export default class PersonModel extends Model {
  @attr title;
  @attr name;

  get fullName() {
    return `${this.title} ${this.name}`;
  }
}
```

### Transforms

You may find the type of an attribute returned by the server does not match the **type** you would like to use in your JavaScript code.Ember Data allows you to define simple `serialization` and `deserialization` methods for attribute types called transforms. *Ember Data supports attribute types of string, number, boolean, and date, which coerce the value to the JavaScript type that matches its name*

```js
import Model, { attr } from '@ember-data/model';

export default class PersonModel extends Model {
  @attr('string') name;
  @attr('number') age;
  @attr('boolean') admin;
  @attr('date') birthday;
}
```

### Custom Transforms

You can also create custom transforms with Ember CLI's transform generator: `ember generate transform dollars`

```js
import Transform from '@ember-data/serializer/transform';

export default class DollarsTransform extends Transform {
  deserialize(serialized) {
    return serialized / 100; // returns dollars
  }

  serialize(deserialized) {
    return deserialized * 100; // returns cents
  }
}
```

A transform has two functions: `serialize` and `deserialize`. Deserialization converts a value to a format that the client expects. Serialization does the reverse and converts a value to the format expected by the persistence layer.

```js
import Model, { attr } from '@ember-data/model';

export default class ProductModel extends Model {
  @attr('dollars') spent;
}
```

### Options

In the following example we define that `verified` has a default value of false and `createdAt` defaults to the current date at the time of the model's creation:

```js
import Model, { attr } from '@ember-data/model';

export default class UserModel extends Model {
  @attr('string') username;
  @attr('string') email;
  @attr('boolean', { defaultValue: false }) verified;
  @attr('date', {
    defaultValue() { return new Date(); }
  }) createdAt;
}
```

### Read-only Attributes ( more to know ?)

When the API returns a deeply nested, read-only object or array, there is no need to create multiple models with attr('hasMany') or attr('belongsTo') relationships. This could result in a potentially large amount of unnecessary code. You can access these objects in the template without transforming them. This can be done by using @attr without specifying a transform:

```js
import Model, { attr } from '@ember-data/model';

export default class PlaceModel extends Model {
  @attr location; // a read-only object
  @attr tags; // a read-only array
}
```

```hbs
{{@model.location.latitude}}
```