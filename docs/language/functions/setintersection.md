# setintersection

[INTENT: REFERENCE]

The `setintersection` function takes multiple sets and produces a single set containing only the elements that all of the given sets have in common. In other words, it computes the intersection of the sets.

## Signature

```hcl
setintersection(first_set, other_sets...)
```

## Parameters

- `first_set` (`set(dynamic)`)
- `other_sets` (`set(dynamic)`, variadic)

## Return type

`set(dynamic)`

Official documentation: [setintersection](https://opentofu.org/docs/language/functions/setintersection/)
