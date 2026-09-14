# pathexpand

[INTENT: REFERENCE]

`pathexpand` takes a filesystem path that might begin with a `~` segment, and if so it replaces that segment with the current user's home directory path.

## Signature

```hcl
pathexpand(path)
```

## Parameters

- `path` (`string`)

## Return type

`string`

Official documentation: [pathexpand](https://opentofu.org/docs/language/functions/pathexpand/)
