# workspace show

[INTENT: REFERENCE]

Show the name of the current workspace.

## Usage

```shell
tofu workspace show
```

## Architectural explanation

`workspace show` prints the name of the currently selected workspace — the minimal read surface for scripts and prompts that need to know which state partition is active.

## Verified example

```shell
tofu workspace show
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox while `verify-ws` was selected: the command printed `verify-ws`.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
