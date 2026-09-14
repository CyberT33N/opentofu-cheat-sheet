# Provider requirements

[INTENT: REFERENCE]

The `required_providers` block inside the `terraform` settings block declares which providers a configuration requires: source address (for example `hashicorp/aws`) and version constraint. `tofu init` installs exactly what is declared, and the [dependency lock file](../files/dependency-lock.md) pins the result. The official language tree carries this topic as a page of the [providers](overview.md) area.

## Official documentation

- [Provider Requirements](https://opentofu.org/docs/language/providers/requirements/)
