# join

[INTENT: REFERENCE]

`join` produces a string by concatenating together all elements of a given list of strings with the given delimiter.

## Signature

```hcl
join(separator, lists...)
```

## Parameters

- `separator` (`string`) — delimiter to insert between the given strings.
- `lists` (`list(string)`, variadic) — one or more lists of strings to join.

## Return type

`string`

Official documentation: [join](https://opentofu.org/docs/language/functions/join/)
