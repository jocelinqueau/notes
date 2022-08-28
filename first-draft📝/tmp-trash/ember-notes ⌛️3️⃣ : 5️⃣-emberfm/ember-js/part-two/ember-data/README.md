# Ember Data

- Ember Data models
- Testing models
- Loading models in routes
- The Ember Data store
- Working with adapters and serializers

## What is Ember Data ?

A while back, we added the rental route. If memory serves us well, we didn't do anything too fancy when we added that new route; we just copy-pasted a lot of the same logic from the index route.

## Ember Data Models

```js
import Model, { attr } from '@ember-data/model';

const COMMUNITY_CATEGORIES = ['Condo', 'Townhouse', 'Apartment'];

export default class RentalModel extends Model {
  @attr title;
  @attr owner;
  @attr city;
  @attr location;
  @attr category;
  @attr image;
  @attr bedrooms;
  @attr description;

  get type() {
    if (COMMUNITY_CATEGORIES.includes(this.category)) {
      return 'Community';
    } else {
      return 'Standalone';
    }
  }
}
```

Attributes declared with the @attr decorator work with the auto-track feature

## Testing Models

`ember generate model-test rental`

We could also have used the ember generate model rental command in the first place, which would have created both the model and test file for us.

`ember generate model rental`

## Loading Models in Routes


## The Ember Data Store

## Working with Adapters and Serializers

*Ember Data uses an adapter and serializer architecture.* **Adapters deal with how and where Ember Data should fetch** data from your servers, such as whether to use HTTP, HTTPS, WebSockets or local storage, as well as the URLs, headers and parameters to use for these requests. **On the other hand, serializers are in charge of converting the data returned by the server into a format Ember Data can understand.**

`app/adapters/application.js`

```js
import JSONAPIAdapter from '@ember-data/adapter/json-api';

export default class ApplicationAdapter extends JSONAPIAdapter {
  namespace = 'api';

  buildURL(...args) {
    return `${super.buildURL(...args)}.json`;
  }
}
```