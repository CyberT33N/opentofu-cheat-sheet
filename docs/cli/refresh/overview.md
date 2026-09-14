# refresh

[INTENT: REFERENCE]

Update the state to match remote systems.

## Usage

```shell
tofu refresh [options]
```

## Options

- `-target=resource` — limit the operation to this resource and its dependencies; repeatable; cannot be used with `-exclude`.
- `-exclude=resource` — limit the operation to everything not excluded or dependent on excluded resources; repeatable; cannot be used with `-target`.
- `-input=true` — ask for input for variables if not directly set.
- `-lock=false` / `-lock-timeout=0s` — state locking control.
- `-parallelism=n` — limit concurrent operations (default 10).
- `-compact-warnings`, `-consolidate-warnings`, `-consolidate-errors` — warning/error presentation control.
- `-concise` — disable progress-related messages.
- `-var 'foo=bar'` / `-var-file=foo` — set input variable values.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-no-color` — disable colored output.
- `-state`, `-state-out`, `-backup` — legacy options supported for the local backend only.

## Architectural explanation

`refresh` updates the state file of the infrastructure with metadata that matches the physical resources being tracked. It does not modify infrastructure, but it can modify the state file — and that updated metadata can cause new changes the next time a plan is generated or applied. In current OpenTofu the same effect is usually reached through `tofu plan -refresh-only` / `apply -refresh-only`; the standalone `refresh` command remains the direct state-update surface.

## Verified example

```shell
tofu refresh -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: both managed instances were refreshed (`Refreshing state...`) and the outputs were re-read from the updated state.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
