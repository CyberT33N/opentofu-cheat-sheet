# providers

[INTENT: NAVIGATION]

Show the providers required for this configuration.

## Usage

```shell
tofu providers [options] [DIR]
```

## Options

- `-test-directory=path` — set the test directory, defaults to `tests`.
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.

## Subcommands

- [lock](lock/overview.md) — Write out dependency locks for the configured providers
- [mirror](mirror/overview.md) — Save local copies of all required provider plugins
- [schema](schema/overview.md) — Show schemas for the providers used in the configuration

## Architectural explanation

Without a subcommand, `providers` prints a tree of the modules in the referenced configuration annotated with their provider requirements, plus the providers required by the state — the overview of why particular provider plugins are needed and why particular versions are selected.

## Verified example

```shell
tofu providers
```

Verified on OpenTofu v1.12.5 (windows_amd64) in the local sandbox: the tree showed `provider[terraform.io/builtin/terraform]` required by the root module, the child module, and the test file, and the state section showed the same built-in provider.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
