# cidrsubnet

[INTENT: REFERENCE]

`cidrsubnet` calculates a subnet address within a given IP network address prefix.

## Signature

```hcl
cidrsubnet(prefix, newbits, netnum)
```

## Parameters

- `prefix` (`string`) — must be given in CIDR notation, as defined in RFC 4632 section 3.1.
- `newbits` (`number`) — the number of additional bits with which to extend the prefix.
- `netnum` (`number`) — a whole number representable with no more than `newbits` binary digits, used to populate the additional bits added to the prefix.

## Return type

`string`

Official documentation: [cidrsubnet](https://opentofu.org/docs/language/functions/cidrsubnet/)
