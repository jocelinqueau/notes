# Component Basics

- Extracting markup into components
- Invoking components
- Passing content to components
- Yielding content with the {{yield}} keyword
- Refactoring existing code
- Writing component tests
- Using the application template and {{outlet}s

## Extracting Markup into Components

example of a simple component

`app/components/jumbo.hbs`
```js
<div class="jumbo">
  <div class="right tomster"></div>
  {{yield}}
</div>
```

## Passing Content to Components with `{{yield}}`

more or less children from react

## Writing Component Tests

`ember generate component-test jumbo`

```js
import { module, test } from 'qunit';
import { setupRenderingTest } from 'ember-qunit';
import { render } from '@ember/test-helpers';
import { hbs } from 'ember-cli-htmlbars';

module('Integration | Component | jumbo', function (hooks) {
  setupRenderingTest(hooks);
  test('it renders the content inside a jumbo header with a tomster', async function (assert) {
    await render(hbs`<Jumbo>Hello World</Jumbo>`);
     assert.dom('.jumbo').exists();
    assert.dom('.jumbo').hasText('Hello World');
    assert.dom('.jumbo .tomster').exists();
  });
});
```

## Using the Application Template and `{{outlet}}`s

like nested component on a route

The {{outlet}} keyword denotes the place where our site's pages should be rendered into, similar to the {{yield}} keyword we saw earlier.

