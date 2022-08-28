# Finding Records

## Retrieving a Single Record

Use `store.findRecord()` to retrieve a record by its type and ID. This will return a promise that fulfills with the requested record:

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

Use `store.findAll()` to retrieve all of the records for a given type:

```js
// GET /blog-posts
this.store.findAll('blog-post') // => GET /blog-posts
  .then(function(blogPosts) {
    // Do something with `blogPosts`
  });
```

Use store.peekAll() to retrieve all of the records for a given type that are already loaded into the store, without making a network request:

```js
let blogPosts = this.store.peekAll('blog-post'); // => no network request
```

store.findAll() returns a PromiseArray that fulfills to a RecordArray and store.peekAll directly returns a RecordArray.

It's important to note that RecordArray is not a JavaScript array, it's an object that implements MutableArray. This is important because, for example, if you want to retrieve records by index, the [] notation will not work--you'll have to use objectAt(index) instead.

## Querying for Multiple Records

Ember Data provides the ability to query for records that meet certain criteria. Calling `store.query()` will make a GET request with the passed object serialized as query params.

```js
// GET to /persons?filter[name]=Peter
this.store.query('person', {
  filter: {
    name: 'Peter'
  }
}).then(function(peters) {
  // Do something with `peters`
});
```

## Querying for A Single Record

???