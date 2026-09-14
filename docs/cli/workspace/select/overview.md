# workspace select

[INTENT: REFERENCE]

Select a workspace.

## Usage

```shell
tofu workspace select [options] NAME
```

## Options

- `-or-create=false` — create the OpenTofu workspace if it does not exist.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

`workspace select` switches the current working directory to a different workspace: all subsequent state operations act on that workspace's state partition. With `-or-create` the selection doubles as a creation path — useful in automation that must land on a workspace whether or not it already exists.

## Verified example

```shell
tofu workspace select default
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: `Switched to workspace "default".`

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
