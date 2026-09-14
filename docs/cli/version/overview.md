# version

[INTENT: REFERENCE]

Show the current OpenTofu version.

## Usage

```shell
tofu version [options]
```

## Options

- `-json` — output the version information as a JSON object.

## Architectural explanation

`version` displays the version of OpenTofu and all installed plugins. The global option `-version` is an alias for this subcommand. It is the first re-anchoring step of any verification workflow: the installed version determines the exact command, flag, and function surface available locally.

## Verified example

```shell
tofu version
```

Verified on the local machine: `OpenTofu v1.12.5 on windows_amd64`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
