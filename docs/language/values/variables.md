# Input variables

[INTENT: REFERENCE]

Input variables are the parameters of an OpenTofu module, declared with the `variable` block and referenced as `var.<NAME>`. Values are assigned through `-var` / `-var-file` CLI options, `terraform.tfvars` and `*.auto.tfvars` files, or defaults in the declaration. The official language tree carries this topic as a page of the [values](overview.md) area.

## Verified example

```hcl
variable "greeting" {
  type    = string
  default = "hello"
}
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the variable was declared with a default, overridden per `-var` on the CLI, and referenced as `var.greeting` in a resource argument.

## Official documentation

- [Input Variables](https://opentofu.org/docs/language/values/variables/)
