# trim

[INTENT: REFERENCE]

`trim` removes the specified set of characters from the start and end of the given string.

## Signature

```hcl
trim(str, cutset)
```

## Parameters

- `str` (`string`)
- `cutset` (`string`) — a string containing all of the characters to trim; each character is taken separately, so the order of characters is insignificant.

## Return type

`string`

Official documentation: [trim](https://opentofu.org/docs/language/functions/trim/)
