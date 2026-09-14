# cidrhost

[INTENT: REFERENCE]

`cidrhost` calculates a full host IP address for a given host number within a given IP network address prefix.

## Signature

```hcl
cidrhost(prefix, hostnum)
```

## Parameters

- `prefix` (`string`) — must be given in CIDR notation, as defined in RFC 4632 section 3.1.
- `hostnum` (`number`) — a whole number representable as a binary integer with no more digits than the address bits remaining after the given prefix.

## Return type

`string`

Official documentation: [cidrhost](https://opentofu.org/docs/language/functions/cidrhost/)
