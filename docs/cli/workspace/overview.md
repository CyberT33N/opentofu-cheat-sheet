# workspace

[INTENT: NAVIGATION]

Workspace management.

## Subcommands

- [delete](delete/overview.md) — Delete a workspace
- [list](list/overview.md) — List Workspaces
- [new](new/overview.md) — Create a new workspace
- [select](select/overview.md) — Select a workspace
- [show](show/overview.md) — Show the name of the current workspace

## Architectural explanation

Workspaces isolate their state: each workspace carries its own state for the same configuration, so one configuration can manage multiple distinct infrastructure sets (for example per environment). The `workspace` command family creates, lists, selects, shows, and deletes these state partitions.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
