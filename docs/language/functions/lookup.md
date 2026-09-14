# lookup

[INTENT: REFERENCE]

`lookup` retrieves the value of a single element from a map, given its key. If the given key does not exist, the given default value is returned instead.

## Signature

```hcl
lookup(inputMap, key, default...)
```

## Parameters

- `inputMap` (`dynamic`)
- `key` (`string`)
- `default` (`dynamic`, variadic, nullable)

## Return type

`dynamic`

Official documentation: [lookup](https://opentofu.org/docs/language/functions/lookup/)
