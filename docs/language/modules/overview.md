# Modules

[INTENT: NAVIGATION]

Modules are containers for multiple resources that are used together. A module consists of a collection of `.tf`, `.tofu`, `.tf.json`, and/or `.tofu.json` files kept together in a directory. Modules are the main way to package and reuse resource configurations with OpenTofu.

Every OpenTofu configuration has at least one module, the _root module_ (the `.tf`/`.tofu` files of the main working directory). A module can _call_ other modules to include their resources; a called module is a _child module_. Child modules can be called multiple times, and multiple configurations can use the same child module. Beyond the local filesystem, OpenTofu loads modules from a public or private registry; the [Public OpenTofu Registry](https://github.com/opentofu/registry/tree/main/modules) hosts a broad collection, and TACOS (TF Automation and Collaboration Software) include a private module registry.

## Pages

- [Module blocks](syntax.md) — the syntax for calling a child module, including meta-arguments
- [Module sources](sources.md) — the paths, addresses, and URIs valid in the `source` argument
- [Module development](develop/overview.md) — developing, composing, and publishing reusable modules

## Verified example

```hcl
module "greeting" {
  source   = "./modules/greeting"
  greeting = var.greeting
}
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the local child module was installed by `tofu get` / `tofu init`, its `terraform_data` resource was created by `tofu apply`, and its output was exported as `module_greeting`.

## Official documentation

- [Modules](https://opentofu.org/docs/language/modules/)
