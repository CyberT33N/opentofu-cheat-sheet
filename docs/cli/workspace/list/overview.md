# workspace list

[INTENT: REFERENCE]

List Workspaces.

## Usage

```shell
tofu workspace list [options]
```

## Options

- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).

## Architectural explanation

`workspace list` lists all OpenTofu workspaces of the current working directory, marking the currently selected workspace with `*`.

## Verified example

```shell
tofu workspace list
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox while `verify-ws` was selected:

```text
  default
* verify-ws
```

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
