# Interactive Components

- Adding behavior to components with classes
- Accessing instance states from templates
- Managing state with tracked properties
- Using conditionals syntaxes in templates
- Responding to user interaction with actions
- Invoking element modifiers
- Testing user interactions

# Adding Behavior to Components with Classes

`ember generate component-class rental/image`

@glimmer/component, or Glimmer component, is one of the several component classes available to use. They are a great starting point whenever you want to add behavior to your components. In this tutorial, we will be using Glimmer components exclusively.

In general, Glimmer components should be used whenever possible. However, you may also see @ember/components, or classic components, used in older apps. You can tell them apart by looking at their import path (which is helpful for looking up the respective documentation, as they have different and incompatible APIs).

```js
import Component from '@glimmer/component';

export default class RentalImageComponent extends Component {
  constructor(...args) {
    super(...args);
    this.isLarge = false;
  }
}
```

```hbs
{{#if this.isLarge}}
  <div class="image large">
    <img ...attributes>
    <small>View Smaller</small>
  </div>
{{else}}
  <div class="image">
    <img ...attributes>
    <small>View Larger</small>
  </div>
{{/if}}
```


**Since this pattern of initializing instance variables in the constructor is pretty common, there happens to be a much more concise syntax for it:**

```js
import Component from '@glimmer/component';

export default class RentalImageComponent extends Component {
  isLarge = false;
}
```

## Managing State with Tracked Properties

```js
import Component from '@glimmer/component';
import { tracked } from '@glimmer/tracking';
import { action } from '@ember/object';

export default class RentalImageComponent extends Component {
  @tracked isLarge = false;

  @action toggleSize() {
    this.isLarge = !this.isLarge;
  }
}
```

## Responding to User Interaction with Actions

```hbs
{{#if this.isLarge}}
<button type="button" class="image large" {{on "click" this.toggleSize}}>
    <img ...attributes>
    <small>View Smaller</small>
    </button>
{{else}}
<button type="button" class="image" {{on "click" this.toggleSize}}>
    <img ...attributes>
    <small>View Larger</small>
</button>
{{/if}}
```

we used the {{on}} modifier to attach this.toggleSize as a click handler on the button.

## Testing User Interactions

`import { render, click } from '@ember/test-helpers';`

Let's clean up our template before moving on. We introduced a lot of duplication when we added the conditional in the template. If we look closely, the only things that are different between the two blocks are:

```hbs
<button type="button" class="image {{if this.isLarge "large"}}" {{on "click" this.toggleSize}}>
  <img ...attributes>
<small>View {{if this.isLarge "Smaller" "Larger"}}</small>
     </button>
```