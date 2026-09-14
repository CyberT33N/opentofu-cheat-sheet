# coalescelist

[INTENT: REFERENCE]

`coalescelist` takes any number of list arguments and returns the first one that isn't empty.

## Signature

```hcl
coalescelist(vals...)
```

## Parameters

- `vals` (`dynamic`, variadic, nullable) — list or tuple values to test in the given order.

## Return type

`dynamic`

Official documentation: [coalescelist](https://opentofu.org/docs/language/functions/coalescelist/)
