# setproduct

[INTENT: REFERENCE]

The `setproduct` function finds all of the possible combinations of elements from all of the given sets by computing the Cartesian product.

## Signature

```hcl
setproduct(sets...)
```

## Parameters

- `sets` (`dynamic`, variadic) — the sets to consider; also accepts lists and tuples, and if all arguments are of list or tuple type then the result preserves the input ordering.

## Return type

`dynamic`

Official documentation: [setproduct](https://opentofu.org/docs/language/functions/setproduct/)
