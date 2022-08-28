# Building pages

## Defining Routes

The place to manage what pages are available is the router. 

```js
import EmberRouter from '@ember/routing/router';
import config from 'super-rentals/config/environment';

export default class Router extends EmberRouter {
  location = config.locationType;
  rootURL = config.rootURL;
}

Router.map(function () {
  this.route('about');
});
```

## Using Route Templates

we can create a new `app/templates/about.hbs` template 

```hbs
<div class="jumbo">
  <div class="right tomster"></div>
  <h2>About Super Rentals</h2>
  <p>
    The Super Rentals website is a delightful project created to explore Ember.
    By building a property rental site, we can simultaneously imagine traveling
    AND building Ember applications.
  </p>
</div>
```

## Defining Routes with Custom Paths

```js
import EmberRouter from '@ember/routing/router';
import config from 'super-rentals/config/environment';

export default class Router extends EmberRouter {
  location = config.locationType;
  rootURL = config.rootURL;
}

Router.map(function () {
  this.route('about');
  this.route('contact', { path: '/getting-in-touch' });
});
```

## Linking Pages with the `<LinkTo>` Component

same as react, `<a href="">` reload the whole app `<LinkTo>` don't

```hbs
<LinkTo @route="about" class="button">About</LinkTo>
```