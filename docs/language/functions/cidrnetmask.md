# cidrnetmask

[INTENT: REFERENCE]

`cidrnetmask` converts an IPv4 address prefix given in CIDR notation into a subnet mask address.

## Signature

```hcl
cidrnetmask(prefix)
```

## Parameters

- `prefix` (`string`) — must be given in CIDR notation, as defined in RFC 4632 section 3.1.

## Return type

`string`

Official documentation: [cidrnetmask](https://opentofu.org/docs/language/functions/cidrnetmask/)
