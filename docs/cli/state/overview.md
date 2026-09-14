# state

[INTENT: NAVIGATION]

Advanced state management.

## Subcommands

- [list](list/overview.md) — List resources in the state
- [mv](mv/overview.md) — Move an item in the state
- [pull](pull/overview.md) — Pull current state and output to stdout
- [push](push/overview.md) — Update remote state from a local state file
- [replace-provider](replace-provider/overview.md) — Replace provider in the state
- [rm](rm/overview.md) — Remove instances from the state
- [show](show/overview.md) — Show a resource in the state

## Architectural explanation

The `state` subcommands slice and dice the OpenTofu state for advanced cases. For safety, all state management commands that modify the state create a timestamped backup of the state prior to making modifications. The structure and output of the commands are tailored to work well with common Unix utilities such as `grep` and `awk`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
