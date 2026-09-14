# base64sha512

[INTENT: REFERENCE]

`base64sha512` computes the SHA512 hash of a given string and encodes it with Base64. This is not equivalent to `base64encode(sha512("test"))` since `sha512()` returns hexadecimal representation.

## Signature

```hcl
base64sha512(str)
```

## Parameters

- `str` (`string`)

## Return type

`string`

Official documentation: [base64sha512](https://opentofu.org/docs/language/functions/base64sha512/)
