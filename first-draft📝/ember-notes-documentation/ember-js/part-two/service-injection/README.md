# Service injection

## splattributes and the class attribute

```hbs
<a
  ...attributes
  href={{this.shareURL}}
  target="_blank"
  rel="external nofollow noopener noreferrer"
  class="share button"
>
  {{yield}}
</a>
```
in this case the class attribute is an exception, it can always be merged


But what happens to the class attribute? Well, as it turns out, the class attribute is the one exception to how these component attributes are overridden! While all other HTML attributes follow the "last-write wins" rule, the values for the class attribute are merged together (concatenated) instead. There is a good reason for this: it allows the component to specify whatever classes that it needs, while allowing the invokers of the component to freely add any extra classes that they need for styling purposes.

## Accessing the Current Page URL

```js
import Component from '@glimmer/component';
const TWEET_INTENT = 'https://twitter.com/intent/tweet';

export default class ShareButtonComponent extends Component {
  get currentURL() {
    return window.location.href;
  }

  get shareURL() {
    let url = new URL(TWEET_INTENT);

    url.searchParams.set('url', this.currentURL);

    if (this.args.text) {
      url.searchParams.set('text', this.args.text);
    }

    if (this.args.hashtags) {
      url.searchParams.set('hashtags', this.args.hashtags);
    }

    if (this.args.via) {
      url.searchParams.set('via', this.args.via);
    }

    return url;
  }
}
```

## Ember Services vs. Global Variables

In Ember, services serve a similar role to global variables, in that they can be easily accessed by any part of your app.

A major difference between services and global variables is that services are scoped to your app, instead of all the JavaScript code that is running on the same page. This allows you to have multiple scripts running on the same page without interfering with each other.

## Mocking Services in Tests
