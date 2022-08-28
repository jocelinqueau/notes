
# Asynchronous Routing -

## The Router Pauses for Promises

When transitioning between routes, the Ember router collects all of the models (via the model hook) that will be passed to the route's controllers at the end of the transition. If the model hook (or the related beforeModel or afterModel hooks) return normal (non-promise) objects or arrays, the transition will complete immediately. But if the model hook (or the related beforeModel or afterModel hooks) returns a promise (or if a promise was provided as an argument to transitionTo), the transition will pause until that promise fulfills or rejects.


If the promise fulfills, the transition will pick up where it left off and begin resolving the next (child) route's model, pausing if it too is a promise, and so on, until all destination route models have been resolved. The values passed to the setupController() hook for each route will be the fulfilled values from the promises.

```js
///app/routes/tardy.js
import Route from '@ember/routing/route';
import { later } from '@ember/runloop';

export default Route.extend({
  model() {
    return new Promise(function(resolve) {
      later(function() {
        resolve({ msg: 'Hold Your Horses' });
      }, 3000);
    });
  },

  setupController(controller, model) {
    console.log(model.msg); // "Hold Your Horses"
  }
});
```

When transitioning into route:tardy, the model() hook will be called and return a promise that won't resolve until 3 seconds later, during which time the router will be paused in mid-transition. When the promise eventually fulfills, the router will continue transitioning and eventually call route:tardy's setupController() hook with the resolved object.

## When Promises Reject...

By default, if a model promise rejects during a transition, the transition is aborted, no new destination route templates are rendered, and an error is logged to the console.
You can handle your error

```js
import Route from '@ember/routing/route';

export default Route.extend({
  model() {
    return Promise.reject("FAIL");
  },

  actions: {
    error(reason) {
      alert(reason); // "FAIL"

      // Can transition to another route here, e.g.
      // this.transitionTo('index');

      // Uncomment the line below to bubble this error event:
      // return true;
    }
  }
});
```

### Recovering from Rejection

Rejected model promises halt transitions, but because promises are chainable, you can catch promise rejects within the model hook itself and convert them into fulfills that won't halt the transition.

```js
import Route from '@ember/routing/route';

export default Route.extend({
  model() {
    return iHopeThisWorks().catch(function() {
      // Promise rejected, fulfill with some default value to
      // use as the route's model and continue on with the transition
      return { msg: 'Recovered from rejected promise' };
    });
  }
});
```