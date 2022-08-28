# Service

> When no arguments are passed, the service is loaded based on the name of the decorated property.

```js
import Component from '@glimmer/component';
import { inject as service } from '@ember/service';

export default class CartContentsComponent extends Component {
  // Will load the service defined in: app/services/shopping-cart.js
  @service shoppingCart;
}
```

Another way to inject a service is to provide the name of the service as an argument to the decorator.

```js
import Component from '@glimmer/component';
import { inject as service } from '@ember/service';

export default class CartContentsComponent extends Component {
  // Will load the service defined in: app/services/shopping-cart.js
  @service('shopping-cart') cart;
}
```

This injects the shopping cart service into the component and makes it available as the cart property.

Sometimes a service may or may not exist, like when an initializer conditionally registers a service. Since normal injection will throw an error if the service doesn't exist, you must look up the service using Ember's getOwner instead.

```js
import Component from '@glimmer/component';
import { getOwner } from '@ember/application';

export default class CartContentsComponent extends Component {
  // Will load the service defined in: app/services/shopping-cart.js
  get cart() {
    return getOwner(this).lookup('service:shopping-cart');
  }
}
```

Injected properties are lazy loaded; meaning the service will not be instantiated until the property is explicitly called.


Once loaded, a service will persist until the application exits.

Below we add a remove action to the cart-contents component.

```js
import Component from '@glimmer/component';
import { inject as service } from '@ember/service';
import { action } from '@ember/object';

export default class CartContentsComponent extends Component {
  @service('shopping-cart') cart;

  @action
  remove(item) {
    this.cart.remove(item);
  }
}
```

Once injected into a component, a service can also be used in the template. Note cart being used below to get data from the cart.

```hbs
<ul>
  {{#each this.cart.items as |item|}}
    <li>
      {{item.name}}
      <button type="button" {{on "click" (fn this.remove item)}}>Remove</button>
    </li>
  {{/each}}
</ul>
```