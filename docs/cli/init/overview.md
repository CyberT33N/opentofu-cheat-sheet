# init

[INTENT: REFERENCE]

Prepare your working directory for other commands.

## Usage

```shell
tofu init [options]
```

## Options

- `-backend=false` — disable backend or cloud backend initialization and use what was previously initialized instead (alias: `-cloud=false`).
- `-backend-config=path` — backend configuration to merge, as an HCL file path or `key=value`; repeatable.
- `-force-copy` — suppress prompts about copying state data when initializing a new state backend.
- `-from-module=SOURCE` — copy the contents of the given module into the target directory before initialization.
- `-get=false` — disable downloading modules for this configuration.
- `-input=false` — disable interactive prompts.
- `-lock=false` — do not hold a state lock during backend migration.
- `-lock-timeout=0s` — duration to retry a state lock.
- `-migrate-state` — reconfigure a backend and attempt to migrate any existing state.
- `-reconfigure` — reconfigure a backend, ignoring any saved configuration.
- `-upgrade` — install the latest module and provider versions allowed within configured constraints, overriding the versions recorded in the dependency lockfile.
- `-lockfile=MODE` — dependency lockfile mode; currently only `readonly` is valid.
- `-plugin-dir` — directory containing plugin binaries; overrides all default search paths and prevents automatic installation; repeatable.
- `-ignore-remote-version` — rare option for cloud/remote backend: ignore local/remote OpenTofu version compatibility checks.
- `-compact-warnings`, `-consolidate-warnings`, `-consolidate-errors` — warning/error presentation control.
- `-test-directory=path` — set the test directory, defaults to `tests`.
- `-json` / `-json-into=out.json` — machine-readable output (to stdout or a file).
- `-var 'foo=bar'` / `-var-file=filename` — set input variable values.
- `-no-color` — disable colored output.

## Architectural explanation

`init` is the first command to run for any new or existing configuration on a machine. It creates the local working directory data (`.terraform`), downloads referenced modules, installs required providers, and initializes the configured backend. It is always safe to run multiple times: it never deletes configuration or state. Validation-grade checks without a remote backend are possible through `tofu init -backend=false`.

## Verified example

```shell
tofu init -backend=false -no-color
```

Verified on OpenTofu v1.12.5 (windows_amd64) against a local sandbox configuration with a local module and the built-in provider: the module was initialized (`- greeting in modules/greeting`), the built-in provider was recognized (`terraform.io/builtin/terraform is built in to OpenTofu`), and initialization completed with `OpenTofu has been successfully initialized!` — fully offline, without any registry access.

Official documentation: [OpenTofu CLI documentation](https://opentofu.org/docs/cli/)
