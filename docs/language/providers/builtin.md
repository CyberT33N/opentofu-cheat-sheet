# Built-in provider

[INTENT: REFERENCE]

The built-in provider `terraform.io/builtin/terraform` ships inside OpenTofu itself — it is never downloaded, never mirrored, and never locked. It provides the `terraform_data` resource (managed values without a remote object), the `terraform_remote_state` data source (reading another configuration's state), and provider-defined functions under `provider::terraform::...`.

## Verified example

Verified on OpenTofu v1.12.5 (windows_amd64) through [`tofu providers schema -json`](../../cli/providers/schema/overview.md) in the local sandbox: the built-in provider registered the functions `provider::terraform::decode_tfvars` (decode a TFVars file into an object), `provider::terraform::encode_tfvars` (encode an object into TFVars format), and `provider::terraform::encode_expr` (convert an expression into a string with valid OpenTofu syntax).

## Official documentation

- [Built-in Provider](https://opentofu.org/docs/language/providers/builtin/)
