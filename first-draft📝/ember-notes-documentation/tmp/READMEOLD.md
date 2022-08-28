# -

### classNameBindings

en gros ternary - to really do
<https://github.com/emberjs/ember.js/issues/13229>

## Javascript classes

<https://guides.emberjs.com/v3.20.0/getting-started/working-with-html-css-and-javascript/#toc_javascript-classes>

### Decorators

Decorators are user defined modifiers that can be applied to a class or class element such as a field or method to change its behavior. For instance, you could create a @cache decorator that caches the return value of a getter the first time it is calculated:

```js
import { cache } from 'my-cache-decorator';

class Counter {
  _count = 0;

  @cache
  get count() {
    return this._count++;
  }
}

let counter = new Counter();

console.log(counter.count); // 0
console.log(counter.count); // 0
```

### later

<https://guides.emberjs.com/v3.20.0/routing/query-params/>
<https://guides.emberjs.com/v3.20.0/routing/preventing-and-retrying-transitions/>
<https://guides.emberjs.com/v3.20.0/routing/loading-and-error-substates/>

###

<br>

# ⏯

<https://guides.emberjs.com/v3.20.0/routing/specifying-a-routes-model/>

## Questions

```js
import Route from '@ember/routing/route';
import { inject as service } from '@ember/service';

export default class FavoritePostsRoute extends Route {
  @service store;

  model() {
    return this.store.findAll('post');
  }
}
```

is `store` in  `@service store` an argument ?

> comment le loading est gerer ?
