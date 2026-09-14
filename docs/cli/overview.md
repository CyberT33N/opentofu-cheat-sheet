# OpenTofu CLI

[INTENT: NAVIGATION]

Complete command tree of the locally installed OpenTofu v1.12.5 (windows_amd64), verified against the local `tofu -help` surface and the [official OpenTofu CLI documentation](https://opentofu.org/docs/cli/).

Every folder below mirrors one command or command group of the CLI, recursively down to the last subcommand.

## Global options

Global options are passed before the subcommand:

- `-chdir=DIR` — switch to a different working directory before executing the given subcommand.
- `-help` — show the top-level help output, or the help for a specified subcommand.
- `-version` — an alias for the `version` subcommand.

## Main commands

- [init](init/overview.md) — Prepare your working directory for other commands
- [validate](validate/overview.md) — Check whether the configuration is valid
- [plan](plan/overview.md) — Show changes required by the current configuration
- [apply](apply/overview.md) — Create or update infrastructure
- [destroy](destroy/overview.md) — Destroy previously-created infrastructure

## All other commands

- [console](console/overview.md) — Try OpenTofu expressions at an interactive command prompt
- [fmt](fmt/overview.md) — Reformat your configuration in the standard style
- [force-unlock](force-unlock/overview.md) — Release a stuck lock on the current workspace
- [get](get/overview.md) — Install or upgrade remote OpenTofu modules
- [graph](graph/overview.md) — Generate a Graphviz graph of the steps in an operation
- [import](import/overview.md) — Associate existing infrastructure with a OpenTofu resource
- [login](login/overview.md) — Obtain and save credentials for a remote host
- [logout](logout/overview.md) — Remove locally-stored credentials for a remote host
- [metadata](metadata/overview.md) — Metadata related commands
- [output](output/overview.md) — Show output values from your root module
- [providers](providers/overview.md) — Show the providers required for this configuration
- [refresh](refresh/overview.md) — Update the state to match remote systems
- [show](show/overview.md) — Show the current state or a saved plan
- [state](state/overview.md) — Advanced state management
- [taint](taint/overview.md) — Mark a resource instance as not fully functional
- [test](test/overview.md) — Execute integration tests for OpenTofu modules
- [untaint](untaint/overview.md) — Remove the 'tainted' state from a resource instance
- [version](version/overview.md) — Show the current OpenTofu version
- [workspace](workspace/overview.md) — Workspace management
