# workspace new

[INTENT: REFERENCE]

Create a new workspace.

## Usage

```shell
tofu workspace new [OPTIONS] NAME
```

## Options

- `-state=path` — copy an existing state file into the new workspace.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

`workspace new` creates a new OpenTofu workspace and switches to it. The new workspace starts with empty state unless `-state` copies an existing state file into it — the cloning path for duplicating an environment's tracked infrastructure into a new partition.

## Verified example

```shell
tofu workspace new verify-ws -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `Created and switched to workspace "verify-ws"!` — with the hint that the new workspace is empty and `tofu plan` will not see any existing state for this configuration.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
