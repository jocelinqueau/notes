
## Loading / Error Substates -

The error and loading substates exist as a part of each route, so they should not be added to your router.js file.

### loading substates

During the beforeModel, model, and afterModel hooks, data may take some time to load. Technically, the router pauses the transition until the promises returned from each hook fulfill.

visual feedback during the transition?

Simply define a template called loading (and optionally a corresponding route) that Ember will transition to. The intermediate transition into the loading substate happens immediately (synchronously), the URL won't be updated, and, unlike other transitions, the currently active transition won't be aborted.

Once the main transition into slow-model completes, the loading route will be exited and the transition to slow-model will continue.

### The loading event

If the various beforeModel/model/afterModel hooks don't immediately resolve, a loading event will be fired on that route.

```js
import Route from '@ember/routing/route';

export default Route.extend({
  model() {
    return this.store.findAll('slow-model');
  },

  actions: {
    loading(transition, originRoute) {
      let controller = this.controllerFor('user');
      controller.set('currentlyLoading', true);

      return true; // allows the loading template to be shown
    }
  }
});
```

If the loading handler is not defined at the specific route, the event will continue to bubble above a transition's parent route, providing the application route the opportunity to manage it.

When using the loading handler, we can make use of the transition promise to know when the loading event is over

```js
import Route from '@ember/routing/route';

export default Route.extend({
  …

  actions: {
    loading(transition, originRoute) {
      let controller = this.controllerFor('user');
      controller.set('currentlyLoading', true);
      transition.promise.finally(function() {
          controller.set('currentlyLoading', false);
      });
    }
  }
});
```

In case we want both custom logic and the default behavior for the loading substate, we can implement the loading action and let it bubble by returning true.

```js
import Route from '@ember/routing/route';

export default Route.extend({
  ...
  actions: {
    loading(transition) {
      let start = new Date();
      transition.promise.finally(() => {
        this.notifier.notify(`Took ${new Date() - start}ms to load`);
      });

      return true;
    }
  }
});
```


### error substates

Ember provides an analogous approach to loading substates in the case of errors encountered during a transition.

The model hooks (beforeModel, model, and afterModel) of an error substate are not called. Only the setupController method of the error substate is called with the error as the model.


Analogous to the loading event, you could manage the error event at the application level to avoid writing the same code for multiple routes.
In case we want to run some custom logic and have the default behavior of rendering the error template, we can handle the error event and let it bubble by returning true.

```js
//app/routes/articles-overview.js

import Route from '@ember/routing/route';

export default Route.extend({
  model(params) {
    return this.get('store').findAll('privileged-model');
  },
  actions: {
    error(error) {
      this.notifier.error(error);

      return true;
    }
  }
});
```
