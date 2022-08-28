# Working With Data

- Working with route files
- Returning local data from the model hook
- Accessing route models from templates
- Mocking server data with static JSON files
- Fetching remote data from the model hook
- Adapting server data
- Loops and local variables in templates with {{#each}}

## Working with Route Files

In Ember, route files are the place to do that. We haven't needed them yet, because all our routes are essentially just rendering static pages up until this point, but we are about to change that.

```js
import Route from '@ember/routing/route';

export default class IndexRoute extends Route {
  async model() {
    return {
      title: 'Grand Old Mansion',
      owner: 'Veruca Salt',
      city: 'San Francisco',
      location: {
        lat: 37.7749,
        lng: -122.4194,
      },
      category: 'Estate',
      type: 'Standalone',
      bedrooms: 15,
      image: 'https://upload.wikimedia.org/wikipedia/commons/c/cb/Crane_estate_(5).jpg',
      description: 'This grand old mansion sits on over 100 acres of rolling hills and dense redwood forests.',
    };
  }
}
```

## Returning Local Data from the Model Hook

## Mocking Server Data with Static JSON Files - Test

put a json on your public folder 


## Adapting Server Data

The rental property objects contained in the array also have a slightly different structure. Every data object has a type and id, which we don't intend to use in our template (yet!). For now, the only data we really need is nested within the attributes key.


**There's one more key difference here, which perhaps only those with very sharp eyes will be able to catch: the data coming from the server is missing the type property, which previously existed on our hard-coded model object. The type property could either be "Standalone" or "Community"**


In Part 2 of this tutorial, we will learn about a more convenient way to consume data in the JSON:API format. For now, we can just fix up the data and deal with these differences in formats ourselves.

```js
import Route from '@ember/routing/route';

const COMMUNITY_CATEGORIES = ['Condo', 'Townhouse', 'Apartment'];

export default class IndexRoute extends Route {
  async model() {
    let response = await fetch('/api/rentals.json');
    let { data } = await response.json();

    return data.map((model) => {
      let { attributes } = model;
      let type;

      if (COMMUNITY_CATEGORIES.includes(attributes.category)) {
        type = 'Community';
      } else {
        type = 'Standalone';
      }

      return { type, ...attributes };
    });
  }
}
```

## Loops and Local Variables in Templates with `{{#each}}`

```hbs
{{#each @model as |rental|}}
      <li><Rental @rental={{rental}} /></li>
    {{/each}}
```