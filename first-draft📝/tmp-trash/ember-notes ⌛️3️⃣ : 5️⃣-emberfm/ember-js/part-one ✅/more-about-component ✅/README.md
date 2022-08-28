# More About Components

- Generating components
- Organizing code with namespaced components
- Forwarding HTML attributes with ...attributes
- Determining the appropriate amount of test coverage

## Generating Components

`ember generate component rental`

## Organizing Code with Namespaced Components

`ember generate component rental/image`

`app/components/rental/image.hbs` which can be invoked as `<Rental::Image>`

## Forwarding HTML Attributes with `...attributes`

```hbs
<div class="image">
  <img ...attributes>
</div>
```

```js
  <Rental::Image
    src="https://upload.wikimedia.org/wikipedia/commons/c/cb/Crane_estate_(5).jpg"
    alt="A picture of Grand Old Mansion"
  />
```

We specified a src and an alt HTML attribute here, which will be passed along to the component and attached to the element where ...attributes is applied in the component template. You can think of this as being similar to {{yield}}

