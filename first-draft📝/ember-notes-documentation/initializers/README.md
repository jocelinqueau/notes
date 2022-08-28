# Initializers

Initializers provide an opportunity to configure your application as it boots.

There are two types of initializers: application initializers and application instance initializers.

Application initializers are run as your application boots, Application instance initializers are run as an application instance is loaded (therefore after)

## Application Initializers

Let's customize the shopping-cart initializer to inject a cart property into all the routes in your application:

```js
export function initialize(application) {
  application.inject('route', 'cart', 'service:shopping-cart');
};

export default {
  initialize
};
```

## Application Instance Initializers

TODO:
