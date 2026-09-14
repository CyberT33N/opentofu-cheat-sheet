# setsubtract

[INTENT: REFERENCE]

The `setsubtract` function returns a new set containing the elements from the first set that are not present in the second set. In other words, it computes the relative complement of the second set.

## Signature

```hcl
setsubtract(a, b)
```

## Parameters

- `a` (`set(dynamic)`)
- `b` (`set(dynamic)`)

## Return type

`set(dynamic)`

Official documentation: [setsubtract](https://opentofu.org/docs/language/functions/setsubtract/)
