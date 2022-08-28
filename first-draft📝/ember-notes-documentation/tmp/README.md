# Finding Records

## Retrieving a Single Record

Use store.findRecord() to retrieve a record by its type and ID. This will return a promise that fulfills with the requested record:

```js
// GET /blog-posts/1
this.store.findRecord('blog-post', 1)  // => GET /blog-posts/1
  .then(function(blogPost) {
      // Do something with `blogPost`
  });
```

Use store.peekRecord() to retrieve a record by its type and ID, without making a network request. This will return the record only if it is already present in the store:

```js
let blogPost = this.store.peekRecord('blog-post', 1); // => no network request
```

## Retrieving Multiple Records

```js
// GET /blog-posts
this.store.findAll('blog-post') // => GET /blog-posts
  .then(function(blogPosts) {
    // Do something with `blogPosts`
  });
```

```js
let blogPosts = this.store.peekAll('blog-post'); // => no network request
```

store.findAll() returns a DS.PromiseArray that fulfills to a DS.RecordArray and store.peekAll directly returns a DS.RecordArray.

## Querying for Multiple Records

