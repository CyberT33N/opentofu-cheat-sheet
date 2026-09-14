# Resources

[INTENT: NAVIGATION]

The `resource` block area of the OpenTofu language: declaring infrastructure objects — the main purpose of the language. Every resource type is implemented by a [provider](../providers/overview.md).

## Pages

- [Resource syntax](syntax.md) — the syntax of the `resource` block
- [Resource behavior](behavior.md) — how OpenTofu creates, updates, and destroys resources
- [terraform_data](tf-data.md) — the built-in `terraform_data` resource
- [Provisioners](provisioners/overview.md) — provisioners and connections

## Verified example

```hcl
resource "terraform_data" "example" {
  input = var.greeting
}
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the resource was planned (`+ create`), created by `tofu apply`, listed by `tofu state list`, and inspected by `tofu state show`.

## Official documentation

- [Resources](https://opentofu.org/docs/language/resources/)
