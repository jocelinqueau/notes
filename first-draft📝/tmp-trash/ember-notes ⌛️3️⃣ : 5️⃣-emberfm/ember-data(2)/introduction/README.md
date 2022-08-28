# Introduction

In Ember Data, models are objects that represent the underlying data that your application presents to the user.Note that Ember Data models are a different concept than the model method on Routes, although they share the same name. Models tend to be persistent.

## Ember Data flexibility

Ember Data can be configured to work with many different kinds of backends. If you need to integrate your Ember.js app with a server that does not have an adapter available (for example, you hand-rolled an API server that does not adhere to any JSON specification), Ember Data is designed to be configurable to work with whatever data your server returns.Ember Data is also designed to work with streaming servers, like those powered by WebSockets. You can open a socket to your server and push changes into Ember Data whenever they occur, giving your app a real-time user interface that is always up-to-date.

## The Store and a Single Source of Truth (like redux)

One common way of building web applications is to tightly couple user interface elements to data fetching. For example, imagine you are writing the admin section of a blogging app, which has a feature that lists the drafts for the currently logged in user.You might be tempted to make the component responsible for fetching that data and storing it:

```javascript
import Component from "@glimmer/component";
import { tracked } from "@glimmer/tracking";
import fetch from "fetch";

export default class ListOfDraftsComponent extends Component {
  @tracked drafts;

  constructor() {
    super(...arguments);

    fetch("/drafts").then((data) => {
      this.drafts = data;
    });
  }
}
```

You could then show the list of drafts in your component's template like this:

```hbs
<ul>
  {{#each this.drafts key="id" as |draft|}}
    <li>{{draft.title}}</li>
  {{/each}}
</ul>
```

This works great for the list-of-drafts component. However, your app is likely made up of many different components. On another page you may want a component to display the number of drafts. You may be tempted to copy and paste your existing willRender code into the new component.

```js
import Component from "@glimmer/component";
import { tracked } from "@glimmer/tracking";
import fetch from "fetch";

export default class DraftsButtonComponent extends Component {
  @tracked drafts;

  constructor() {
    super(...arguments);

    fetch("/drafts").then((data) => {
      this.drafts = data;
    });
  }
}
```

Unfortunately, the app will now make two separate requests for the same information. **Not only is the redundant data fetching costly in terms of wasted bandwidth and affecting the perceived speed of your app, it's easy for the two values to get out-of-sync.**

### Injecting the store

Ember Data provides a store service that you can inject into routes, components, services and other classes, that enables you to access the store directly.

```js
import Route from "@ember/routing/route";
import { service } from "@ember/service";

export default class BlogPostsIndexRoute extends Route {
  @service store;

  model() {
    return this.store.findAll("posts");
  }
}
```

## Models

In Ember Data, each model is represented by a subclass of Model that defines the attributes, relationships, and behavior of the data that you present to the user.

```js
import Model, { attr } from "@ember-data/model";

export default class PersonModel extends Model {
  @attr("string") name;
  @attr("date") birthday;
}
```

**A model also describes its relationships with other objects. For example, an order may have many line-items, and a line-item may belong to a particular order.**

```js
import Model, { hasMany } from "@ember-data/model";

export default class OrderModel extends Model {
  @hasMany("line-item") lineItems;
}
```

```js
import Model, { belongsTo } from "@ember-data/model";

export default class LineItemModel extends Model {
  @belongsTo("order") order;
}
```

Models don't have any data themselves, they define the attributes, relationships and behavior of specific instances, which are called records.

## Records (collection of structured data)

A record is an instance of a model that contains data loaded from a server. Your application can also create new records and save them back to the server. A record is uniquely identified by its model type and ID.

```js
this.store.findRecord("person", 1); // => { id: 1, name: 'steve-buscemi' }
```

## Adapter

An adapter is an object that translates requests from Ember (such as "find the user with an ID of 1") into requests to a server.

## Caching

The store will automatically cache records for you. If a record had already been loaded, asking for it a second time will always return the same object instance.

*—always returning the same record object, no matter how many times you look it up—is sometimes called an identity map.*

One downside to returning a cached record is you may find the state of the data has changed since it was first loaded into the store's identity map. In order to prevent this stale data from being a problem for long, Ember Data will automatically make a request in the background each time a cached record is returned from the store. When the new data comes in, the record is updated, and if there have been changes to the record since the initial render, the template is re-rendered with the new information.
