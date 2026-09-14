# cidrcontains

[INTENT: REFERENCE]

`cidrcontains` determines whether a given IP address or an address prefix given in CIDR notation is within a given IP network address prefix.

## Signature

```hcl
cidrcontains(containing_prefix, contained_ip_or_prefix)
```

## Parameters

- `containing_prefix` (`string`) — must be given in CIDR notation, as defined in RFC 4632 section 3.1.
- `contained_ip_or_prefix` (`string`) — either an IP address or an address prefix given in CIDR notation.

## Return type

`bool`

Official documentation: [cidrcontains](https://opentofu.org/docs/language/functions/cidrcontains/)
