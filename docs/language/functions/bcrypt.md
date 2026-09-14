# bcrypt

[INTENT: REFERENCE]

`bcrypt` computes a hash of the given string using the Blowfish cipher, returning a string in the Modular Crypt Format usually expected in the shadow password file on many Unix systems.

## Signature

```hcl
bcrypt(str, cost...)
```

## Parameters

- `str` (`string`)
- `cost` (`number`, variadic, optional) — the cost argument; defaults to 10 if unspecified.

## Return type

`string`

Official documentation: [bcrypt](https://opentofu.org/docs/language/functions/bcrypt/)
