# Reusable Components

- Managing application-level configurations
- Parameterizing components with arguments
- Accessing component arguments
- Interpolating values in templates
- Overriding HTML attributes in ...attributes
- Refactoring with getters and auto-track
- Getting JavaScript values into the test context

## Managing Application-level Configurations

## Generating a Component with a Component Class

`ember generate component map --with-component-class`

`ember g component map -gc`

## Parameterizing Components with Arguments

## Interpolating Values in Templates

```hbs
<div class="map">
  <img
    alt="Map image at coordinates {{@lat}},{{@lng}}"
    ...attributes
    src="https://api.mapbox.com/styles/v1/mapbox/streets-v11/static/{{@lng}},{{@lat}},{{@zoom}}/{{@width}}x{{@height}}@2x?access_token={{this.token}}"
    width={{@width}} height={{@height}}
  >
</div>
```

allow alt to be override

## Overriding HTML Attributes in ...attributes

```hbs
 <Map
    @lat="37.7749"
    @lng="-122.4194"
    @zoom="9"
    @width="150"
    @height="150"
    alt="A map of Grand Old Mansion"
  />
```

## Refactoring with Getters and Auto-track

```js
import Component from '@glimmer/component';
import ENV from 'super-rentals/config/environment';

const MAPBOX_API = 'https://api.mapbox.com/styles/v1/mapbox/streets-v11/static';

export default class MapComponent extends Component {
  get src() {
    let { lng, lat, width, height, zoom } = this.args;

    let coordinates = `${lng},${lat},${zoom}`;
    let dimensions = `${width}x${height}`;
    let accessToken = `access_token=${this.token}`;

    return `${MAPBOX_API}/${coordinates}/${dimensions}@2x?${accessToken}`;
  }

  get token() {
    return encodeURIComponent(ENV.MAPBOX_ACCESS_TOKEN);
  }
}
```

```hbs
<div class="map">
  <img
    alt="Map image at coordinates {{@lat}},{{@lng}}"
    ...attributes
    src={{this.src}}
    width={{@width}} height={{@height}}
  >
</div>
```