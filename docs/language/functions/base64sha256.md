# base64sha256

[INTENT: REFERENCE]

`base64sha256` computes the SHA256 hash of a given string and encodes it with Base64. This is not equivalent to `base64encode(sha256("test"))` since `sha256()` returns hexadecimal representation.

## Signature

```hcl
base64sha256(str)
```

## Parameters

- `str` (`string`)

## Return type

`string`

Official documentation: [base64sha256](https://opentofu.org/docs/language/functions/base64sha256/)
