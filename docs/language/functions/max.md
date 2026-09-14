# max

[INTENT: REFERENCE]

`max` takes one or more numbers and returns the greatest number from the set.

## Signature

```hcl
max(numbers...)
```

## Parameters

- `numbers` (`number`, variadic)

## Return type

`number`

## Verified example

```shell
echo 'max(1,2)' | tofu console
```

Verified on OpenTofu v1.12.5 (windows_amd64): the console printed `2`.

Official documentation: [max](https://opentofu.org/docs/language/functions/max/)
