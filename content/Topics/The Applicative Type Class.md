## Definition

```haskell
class Functor m => Applicative m where
    pure :: a -> m a
    (<$>) :: m (a -> b) -> m a -> m b
```

As you notice, to define something as an `Applicative` it must already be defined as a [[The Functor Type Class| Functor]].
