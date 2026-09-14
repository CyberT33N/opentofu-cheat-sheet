# Workspaces

[INTENT: REFERENCE]

Workspaces are state partitions of one configuration: each workspace carries its own state, so the same configuration can manage multiple distinct infrastructure sets. They are managed through the [`tofu workspace`](../../cli/workspace/overview.md) command family. The official language tree carries this topic as a page of the [state](overview.md) area.

## Verified example

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `tofu workspace new verify-ws` created an isolated empty state partition, and `tofu workspace list` marked the selected workspace with `*`.

## Official documentation

- [Workspaces](https://opentofu.org/docs/language/state/workspaces/)
