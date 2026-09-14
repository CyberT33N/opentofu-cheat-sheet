# metadata functions

[INTENT: REFERENCE]

Show signatures and descriptions for the available functions.

## Usage

```shell
tofu metadata functions -json
```

## Options

- `-json` — mandatory: prints out a JSON representation of the available function signatures.

## Architectural explanation

`metadata functions` exposes the complete built-in function catalog of the installed OpenTofu version as machine-readable data: for every function its description, return type, positional parameters, and variadic parameter. This is the programmatic single source of truth behind the [language function reference](../../language/functions/overview.md). The catalog lists every function twice: once under its plain name and once under its `core::` namespaced alias.

## Verified example

```shell
tofu metadata functions -json
```

Verified on OpenTofu v1.12.5 (windows_amd64): the JSON document (`format_version: "1.0"`) carries the signatures of all 121 built-in functions, each both as plain name and as `core::`-prefixed alias.

## Troubleshooting

- `tofu metadata functions` without `-json` fails with `Invalid arguments` — the command requires the `-json` flag; there is no human-readable output mode.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
