# matchkeys

[INTENT: REFERENCE]

`matchkeys` constructs a new list by taking a subset of elements from one list whose indexes match the corresponding indexes of values in another list.

## Signature

```hcl
matchkeys(values, keys, searchset)
```

## Parameters

- `values` (`list(dynamic)`)
- `keys` (`list(dynamic)`)
- `searchset` (`list(dynamic)`)

## Return type

`list(dynamic)`

Official documentation: [matchkeys](https://opentofu.org/docs/language/functions/matchkeys/)
