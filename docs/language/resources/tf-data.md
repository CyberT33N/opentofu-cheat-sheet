# terraform_data

[INTENT: REFERENCE]

The built-in `terraform_data` resource of the [built-in provider](../providers/builtin.md): stores a managed value (`input` in, `output` out) without any remote object — useful for triggers, placeholders, and values that need a resource lifecycle. It supports import with an arbitrary ID.

## Verified example

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `terraform_data.example` was created by `tofu apply` with `input = "hello"`, re-imported through [`tofu import`](../../cli/import/overview.md) with an arbitrary ID (`Import successful!`), and destroyed by `tofu destroy`.

## Official documentation

- [terraform_data](https://opentofu.org/docs/language/resources/tf-data/)
