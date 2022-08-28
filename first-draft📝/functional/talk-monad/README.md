# Talk If you know map, I will teach you monads

[Nordic.js 2016 • Mattias Petter Johansson - If you know map, I will teach you monads](https://www.youtube.com/watch?v=2jp8N6Ha7tY)

` A functor is something that you can map`

` A monad is something that you can flatMap`

4 different functor

Array - tree - Stream - Promise

Stream and Promise are monad

flatMap is just like map, except flatMap does not expect the mapper to return a value

instead flatMap expect the mapper to return a functor containing the value, and flatMap will take that functor anf flatten into it's actual value