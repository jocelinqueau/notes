# Redirecting

One of the methods is transitionTo(). Calling transitionTo() from a route or transitionToRoute() from a controller will stop any transitions currently in progress and start a new one, functioning as a redirect. transitionTo() behaves exactly like the LinkTo helper.

The other one is replaceWith() which works the same way as transitionTo(). The only difference between them is how they manage history. replaceWith() substitutes the current route entry and replaces it with that of the route we are redirecting to, while transitionTo() leaves the entry for the current route and creates a new one for the redirection.

If the new route has dynamic segments, you need to pass either a model or an identifier for each segment.

## Transitioning Before the Model is Known

Since a route's beforeModel() executes before the model() hook, it's a good place to do a redirect if you don't need any information that is contained in the model.

```js
import Route from '@ember/routing/route';

export default class IndexRoute extends Route {
  beforeModel(/* transition */) {
    this.transitionTo('posts'); // Implicitly aborts the on-going transition.
  }
}
```

beforeModel() receives the current transition as an argument, which we can store and retry later. This allows us to return the user back to the original route. For example, we might redirect a user to the login page when they try to edit their profile, and immediately redirect them back to the edit page once they have successfully logged in.

<https://guides.emberjs.com/v3.20.0/routing/preventing-and-retrying-transitions/#toc_storing-and-retrying-a-transition>

## Transitioning After the Model is Known

If you need information about the current model in order to decide about redirection, you can use the afterModel() hook. It receives the resolved model as the first parameter and the transition as the second one.

```js
import Route from '@ember/routing/route';

export default class PostsRoute extends Route {
  afterModel(model, transition) {
    if (model.get('length') === 1) {
      this.transitionTo('post', model.get('firstObject'));
    }
  }
}
```

> If you attempt to redirect with the `queryParams` option, make sure that the query params are defined on the controller!

### Child Routes

we can use the `redirect()` method, which will leave the original transition validated, ??

## Preventing and Retrying Transitions -

During a route transition, the Ember Router passes a transition object to the various hooks on the routes involved in the transition. Any hook that has access to this transition object has the ability to immediately abort the transition by calling transition.abort(), and if the transition object is stored, it can be re-attempted at a later time by calling transition.retry().

### Preventing Transitions via willTransition

When a transition is attempted, whether via <LinkTo />, transitionTo, or a URL change, a willTransition action is fired on the currently active routes. This gives each active route, starting with the leaf-most route, the opportunity to decide whether or not the transition should occur.

`prevent losing user form data`

```js
import Route from '@ember/routing/route';
import { action } from '@ember/object';

export default class FormRoute extends Route {
  @action
  willTransition(transition) {
    if (this.controller.userHasEnteredData &&
        !confirm('Are you sure you want to abandon progress?')) {
      transition.abort();
    } else {
      // Bubble the `willTransition` action so that
      // parent routes can decide whether or not to abort.
      return true;
    }
  }
};
```

> transition bubble up

However, if the browser back button is used to navigate away from route:form, or if the user manually changes the URL, the new URL will be navigated to before the willTransition action is called. This will result in the browser displaying the new URL, even if willTransition calls transition.abort().

## Aborting Transitions Within model, beforeModel, afterModel
