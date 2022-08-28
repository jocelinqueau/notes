# Mirage

> url <https://www.ember-cli-mirage.com/docs/getting-started/overview#serializers>

Mirage is a JavaScript library that lets frontend developers mock out backend APIs.

Unlike other mocking libraries, Mirage makes it easy to reproduce dynamic scenarios that are typically only possible when using a true production server.

Equipped with a Mirage server, a frontend developer can build, test, and even share a complete working Ember application without having to use or configure any backend services.

## route handlers

```js
// mirage/config.js
export default function() {
  this.namespace = 'api';

  this.get('/movies', () => {
    return {
      data: [
        { id: 1, type: 'movies', attributes: { name: 'Interstellar' } },
        { id: 2, type: 'movies', attributes: { name: 'Inception' } },
        { id: 3, type: 'movies', attributes: { name: 'Dunkirk' } },
      ]
    };
  });

}
```

### creating a model

> `ember g mirage-model movie`

```js
// mirage/models/movie.js
import { Model } from 'miragejs';

export default Model.extend({
});
```

### Writing a dynamic route handler

Let's update our route handler (to be dynamic):

```js
this.get('/movies', (schema, request) => {
  return schema.movies.all();
});
```

The schema argument lets us access our new Movie model. This route will now respond with all the authors in Mirage's database at the time of the request.

### Seeding the database

Right now

```js
// GET /api/movies
data: [
]
```

That's because Mirage's database is empty.

To actually seed our database with fake data, we'll use factories. Factories are objects that make it easy to generate realistic-looking data for your Mirage server.

> `ember g mirage-factory movie`

We can then define some properties on our Factory, Booleans, Strings or Numbers, or functions that return dynamic data etc (faker for example)

```js
// mirage/factories/movie.js
import { Factory } from 'miragejs';

export default Factory.extend({

  title(i) {
    return `Movie ${i}`; // Movie 1, Movie 2, etc.
  },

  year() {
    let min = 1950;
    let max = 2019;

    return Math.floor(Math.random() * (max - min + 1)) + min;
  },

  rating: "PG-13"

});
```

The database **will assign each record an id**, and now we can interact with this data in our route handlers

To actually use our new factory definition, we can call the server.create and server.createList methods.

To seed our development database, use the function in the scenarios/default.js file:

```js
// mirage/scenarios/default.js
export default function(server) {

  server.createList('movie', 10);

};
```

In acceptance tests, scenarios/default.js is ignored, and instead you can use this.server to setup your database in the state needed for the test:

```js
// tests/acceptance/movies-test.js
import { setupApplicationTest } from 'ember-qunit';
import { setupMirage } from 'ember-cli-mirage/test-support';

module('Acceptance | Homepage test', function(hooks) {
  setupApplicationTest(hooks);
  setupMirage(hooks);

  test("I can view the movies", async function(assert) {
    this.server.createList("movie", 3);

    await visit("/home");

    assert.dom("[data-test-id='movie-row']").exists({ count: 3 });
  });
});
```

You can also pass attribute overrides directly to create or createList

```js
test("I can view the movie title", async function(assert) {
  let movie = this.server.create('movie', { title: "Interstellar" });

  await visit(`/movies/${movie.id}`);

  assert.dom('h1').includesText("Interstellar");
});
```

## Associations

Dealing with associations is always tricky, and faking endpoints that deal with associations is no exception. Fortunately, Mirage ships with an ORM to help keep your route handlers clean.

Let's say your movie has many cast-members. You can declare this relationship in your model:

> pretty much like Active record(rails orm)

```js
// mirage/models/movie.js
import { Model, hasMany } from 'miragejs';

export default Model.extend({
  castMembers: hasMany()
});

// mirage/models/cast-member.js
import { Model, belongsTo } from 'miragejs';

export default Model.extend({
  movie: belongsTo()
});

```

```js
this.get('/movies/:id/cast-members', (schema, request) => {
  let movie = schema.movies.find(request.params.id);

  return movie.castMembers;
});
```

## Serializers TBD

TODO:
