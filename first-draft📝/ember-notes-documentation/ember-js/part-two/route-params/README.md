# Route Params

## Routes with Dynamic Segments

`this.route('rental', { path: '/rentals/:rental_id' })`

a :rental_id, which is what we call a dynamic segment. 

## Links with Dynamic Segments

```hbs
 <h3>
      <LinkTo @route="rental" @model={{@rental}}>
        {{@rental.title}}
      </LinkTo>
    </h3>
```

Since we know that we're linking to the rental route that we just created, we also know that this route requires a dynamic segment. Thus, we need to pass in a `@model` argument so that the `<LinkTo>` component can generate the appropriate URL for that model.

**model need id**

*route for a paramtimideze*

```js
import Route from '@ember/routing/route';

const COMMUNITY_CATEGORIES = ['Condo', 'Townhouse', 'Apartment'];

export default class RentalRoute extends Route {
  async model(params) {
    let response = await fetch(`/api/rentals/${params.rental_id}.json`);
    let { data } = await response.json();

    let { id, attributes } = data;
    let type;

    if (COMMUNITY_CATEGORIES.includes(attributes.category)) {
      type = 'Community';
    } else {
      type = 'Standalone';
    }

    return { id, type, ...attributes };
  }
}
```