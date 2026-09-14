# Providers

[INTENT: NAVIGATION]

OpenTofu relies on plugins called providers to interact with cloud providers, SaaS providers, and other APIs. Each provider adds a set of [resource types](../resources/overview.md) and/or [data sources](../data-sources/overview.md) that OpenTofu can manage; without providers, OpenTofu cannot manage any kind of infrastructure. Providers are distributed separately from OpenTofu itself, each with its own release cadence and version numbers; the [Public OpenTofu Registry](https://registry.opentofu.org/) is the main directory of publicly available providers. In production, constraining acceptable provider versions in the provider requirements block is recommended so that `tofu init` does not install incompatible newer versions.

## Pages

- [Provider requirements](requirements.md) — declaring which providers a configuration requires
- [Provider configuration](configuration.md) — configuring provider settings
- [Built-in provider](builtin.md) — the `terraform.io/builtin/terraform` built-in provider

## Verified example

The local sandbox configuration ran entirely on the built-in provider: `tofu init` reported `terraform.io/builtin/terraform is built in to OpenTofu`, and [`tofu providers schema -json`](../../cli/providers/schema/overview.md) showed its `terraform_data` resource, its `terraform_remote_state` data source, and its three provider-defined functions.

## Official documentation

- [Providers](https://opentofu.org/docs/language/providers/)
