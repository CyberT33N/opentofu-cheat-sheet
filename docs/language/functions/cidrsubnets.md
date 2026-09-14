# cidrsubnets

[INTENT: REFERENCE]

`cidrsubnets` calculates a sequence of consecutive IP address ranges within a particular CIDR prefix.

## Signature

```hcl
cidrsubnets(prefix, newbits...)
```

## Parameters

- `prefix` (`string`) — must be given in CIDR notation, as defined in RFC 4632 section 3.1.
- `newbits` (`number`, variadic) — the number of additional bits for each successive subnet.

## Return type

`list(string)`

Official documentation: [cidrsubnets](https://opentofu.org/docs/language/functions/cidrsubnets/)
