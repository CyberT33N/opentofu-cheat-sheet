# providers schema

[INTENT: REFERENCE]

Show schemas for the providers used in the configuration.

## Usage

```shell
tofu providers schema [options] -json
```

## Options

- `-json` — mandatory: prints out a JSON representation of the schemas for all providers used in the current configuration.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.

## Architectural explanation

`providers schema -json` dumps the full schema of every provider used in the current configuration: provider block, resource schemas, data source schemas, and — since provider-defined functions exist — the `functions` a provider registers. This is the machine-readable contract surface for tooling, editors, and schema-driven validation.

## Verified example

```shell
tofu providers schema -json
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the JSON document carries the built-in provider `terraform.io/builtin/terraform` with the `terraform_data` resource schema, the `terraform_remote_state` data source schema, and three provider-defined functions (`provider::terraform::decode_tfvars`, `provider::terraform::encode_expr`, `provider::terraform::encode_tfvars`).

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
