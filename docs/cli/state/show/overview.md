# state show

[INTENT: REFERENCE]

Show a resource in the state.

## Usage

```shell
tofu state show [options] ADDRESS
```

## Options

- `-state=statefile` — path to a state file to look up resources; by default the state `terraform.tfstate` is used if it exists.
- `-show-sensitive` — display sensitive values.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file). Warning: these options always print sensitive values, even if `-show-sensitive` is not specified.

## Architectural explanation

`state show` shows the attributes of a single resource in the OpenTofu state. The address argument must specify a single resource; available resources can be listed with [state list](../list/overview.md). It is the per-resource inspection surface of the state — the read model for one managed object.

## Verified example

```shell
tofu state show terraform_data.example -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the resource was rendered with its attributes — `id = "<RESOURCE_ID>"`, `input = "hello"`, `output = "hello"`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
