# Dependency lock file

[INTENT: REFERENCE]

The dependency lock file (`.terraform.lock.hcl`) records the exact provider versions and checksums a configuration is locked to, so that every installation uses the same provider packages. It is written by `tofu init` and maintained explicitly through [`tofu providers lock`](../../cli/providers/lock/overview.md). The official language tree carries this topic as a page of the [files](overview.md) area.

## Official documentation

- [Dependency Lock File](https://opentofu.org/docs/language/files/dependency-lock/)
