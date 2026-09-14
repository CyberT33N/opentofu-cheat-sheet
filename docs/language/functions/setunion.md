# setunion

[INTENT: REFERENCE]

The `setunion` function takes multiple sets and produces a single set containing the elements from all of the given sets. In other words, it computes the union of the sets.

## Signature

```hcl
setunion(first_set, other_sets...)
```

## Parameters

- `first_set` (`set(dynamic)`)
- `other_sets` (`set(dynamic)`, variadic)

## Return type

`set(dynamic)`

Official documentation: [setunion](https://opentofu.org/docs/language/functions/setunion/)
