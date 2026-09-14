# state list

[INTENT: REFERENCE]

List resources in the state.

## Usage

```shell
tofu state list [options] [address...]
```

Aliases: `state ls`.

## Options

- `-state=statefile` — path to a state file to look up resources; by default the state of the currently selected workspace is consulted.
- `-id=ID` — filter results to instances whose resource types have an `id` attribute equal to the given string.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

`state list` lists resource instances in the OpenTofu state. The optional address arguments filter instances by resource or module; without a pattern, all instances are listed. Filter addresses must be module addresses or absolute resource addresses (for example `module.example` or `module.example.aws_instance.example`); an error is returned if a given filter address does not exist in the state.

## Verified example

```shell
tofu state list
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: after [apply](../../apply/overview.md) the command listed `terraform_data.example` and `module.greeting.terraform_data.this`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
