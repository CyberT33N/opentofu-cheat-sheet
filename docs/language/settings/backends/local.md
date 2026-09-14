# local backend

[INTENT: REFERENCE]

The `local` backend stores the OpenTofu state on the local filesystem (`terraform.tfstate`) — the default when no backend is configured. The official language tree carries this backend as a page of the [backends](overview.md) area.

## Verified example

The entire local sandbox verification of this cheat sheet ran on the local backend: `terraform.tfstate` in the working directory, written by `tofu apply`, read by [`tofu state pull`](../../../cli/state/pull/overview.md), and overwritten by [`tofu state push`](../../../cli/state/push/overview.md).

## Official documentation

- [local Backend](https://opentofu.org/docs/language/settings/backends/local/)
