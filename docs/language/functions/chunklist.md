# chunklist

[INTENT: REFERENCE]

`chunklist` splits a single list into fixed-size chunks, returning a list of lists.

## Signature

```hcl
chunklist(list, size)
```

## Parameters

- `list` (`list(dynamic)`)
- `size` (`number`) — the maximum length of each chunk; all but the last element of the result are guaranteed to be of exactly this size.

## Return type

`list(list(dynamic))`

Official documentation: [chunklist](https://opentofu.org/docs/language/functions/chunklist/)
