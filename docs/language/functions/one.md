# one

[INTENT: REFERENCE]

`one` takes a list, set, or tuple value with either zero or one elements. If the collection is empty, `one` returns `null`. Otherwise, `one` returns the first element. If there are two or more elements then `one` will return an error.

## Signature

```hcl
one(list)
```

## Parameters

- `list` (`dynamic`)

## Return type

`dynamic`

Official documentation: [one](https://opentofu.org/docs/language/functions/one/)
