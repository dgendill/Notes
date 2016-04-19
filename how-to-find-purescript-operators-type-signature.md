# How do I find the type of a operator in PureScript?
# How do I find the type of a user defined operator in PureScript?

You can use the :type command in psci, and put the operator in parenthesis. e.g.

```
> :type (++)
forall s. (Semigroup s) => s -> s -> s

> Import Data.Array
> :type (..)
Int -> Int -> Array Int
```

# How do I find the 'fixity declaration', aka 'user defind operator', aka 'operator alias' for a PureScript function?

# How do I find the PureScript function associated with an 'operator alias', for example "++" (append) or ".." (range)?

As of 4/19, this is currently a requested feature https://github.com/purescript/purescript/issues/1136
