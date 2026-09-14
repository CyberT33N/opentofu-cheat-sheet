# workspace delete

[INTENT: REFERENCE]

Delete a workspace.

## Usage

```shell
tofu workspace delete [options] NAME
```

## Options

- `-force` — remove a workspace even if it is managing resources (OpenTofu can then no longer track or manage the workspace's infrastructure).
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

`workspace delete` deletes a OpenTofu workspace and its state partition. Without `-force` the deletion is refused when the workspace still manages resources — the guard against orphaning tracked infrastructure.

## Verified example

```shell
tofu workspace delete verify-ws -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `Deleted workspace "verify-ws"!` — after switching back to `default` (see [workspace select](../select/overview.md)).

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
