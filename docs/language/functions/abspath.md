# abspath

[INTENT: REFERENCE]

`abspath` takes a string containing a filesystem path and converts it to an absolute path. That is, if the path is not absolute, it will be joined with the current working directory.

## Signature

```hcl
abspath(path)
```

## Parameters

- `path` (`string`)

## Return type

`string`

Official documentation: [abspath](https://opentofu.org/docs/language/functions/abspath/)
